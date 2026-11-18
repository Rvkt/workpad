---
title: "Optimizing React Native Performance: A Developer's Guide"
source: "https://dev.to/ajmal_hasan/optimizing-react-native-performance-a-developers-guide-3hd1"
author:
  - "[[Ajmal Hasan]]"
published: 2025-03-19
created: 2026-10-22
description: "As a React Native developer with years of experience, I've compiled my most valuable performance... Tagged with reactnative, javascript, mobile."
tags:
  - "clippings"
hub: "[[Clippings]]"
---

> [!info] 🔗 **Clipping Hub:** [[Clippings]] · **Related:** [[Performance Overview · React Native]], [[react-native-toast-message|react-native-toast-message]] · **Topic:** [[DroidLens|DroidLens]]

As a React Native developer with years of experience, I've compiled my most valuable performance optimization techniques into this comprehensive guide. Save it for later and evaluate your projects against these battle-tested practices!

This e-book is best for detailed info. Check out [Callstack E-Book](https://www.callstack.com/ebook/the-ultimate-guide-to-react-native-optimization)

## Code Optimization

### 1\. Don't rely on useMemo & useCallback too much

Design your components to minimize memoization needs instead of defaulting to these hooks.

```
// Instead of excessive memoization:
const handlePress = useCallback(() => {
  navigateToProfile(user.id);
}, [user.id]);

// Consider if the simple approach works for your case:
const handlePress = () => navigateToProfile(user.id);
```

Memoization itself has a performance cost. For most components, the overhead of recreating functions is negligible compared to the cost of tracking dependencies.

### 2\. Don't rely on custom hooks too much

Custom hooks improve readability, not performance. Each instance uses separate resources.

```
// Each component using this creates separate instances
const useCounter = () => {
  const [count, setCount] = useState(0);
  return {
    count,
    increment: () => setCount(prev => prev + 1)
  };
};

// Better for widely-used functionality:
const globalCounter = {
  count: 0,
  listeners: new Set(),
  increment() {
    this.count++;
    this.listeners.forEach(listener => listener(this.count));
  },
  subscribe(listener) {
    this.listeners.add(listener);
    return () => this.listeners.delete(listener);
  }
};
```

### 3\. Keep files small (~200 lines, including stylesheet)

Smaller files improve readability, maintainability, and compilation speed.

```
// ProfileScreen.js (~200 lines including styles)
import ProfileHeader from './ProfileHeader';
import ProfileContent from './ProfileContent';

const ProfileScreen = () => (
  <View style={styles.container}>
    <ProfileHeader />
    <ProfileContent />
  </View>
);

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#fff'
  }
});
```

### 4\. Follow SOLID (Single Responsibility)

Components should get data directly instead of through prop chains.

```
// Instead of prop drilling:
<App>
  <MainScreen>
    <Dashboard>
      <UserInfo userData={userData} />
    </Dashboard>
  </MainScreen>
</App>

// Better approach with direct access:
const UserInfo = () => {
  const { userData } = useUserContext(); // Or Redux/MobX/etc.
  return <Text>{userData.name}</Text>;
};
```

### 5\. Use useRef instead of useState if it doesn't reflect on the UI

For values that don't trigger re-renders, useRef is more efficient.

```
// Bad - causes re-renders when scrollPosition changes
const [scrollPosition, setScrollPosition] = useState(0);
const handleScroll = (event) => {
  setScrollPosition(event.nativeEvent.contentOffset.y);
};

// Good - no re-renders until needed
const scrollPositionRef = useRef(0);
const handleScroll = (event) => {
  scrollPositionRef.current = event.nativeEvent.contentOffset.y;
  if (scrollPositionRef.current > threshold) {
    // Only update state when needed
    setShowHeader(false);
  }
};
```

### 6\. Avoid inline styles, use StyleSheet

StyleSheet provides optimization and better performance.

```
// Bad
<View style={{ padding: 10, margin: 15, backgroundColor: '#fff' }}>
  <Text style={{ color: 'black', fontSize: 16 }}>Hello World</Text>
</View>

// Good
<View style={styles.container}>
  <Text style={styles.text}>Hello World</Text>
</View>

const styles = StyleSheet.create({
  container: {
    padding: 10,
    margin: 15,
    backgroundColor: '#fff'
  },
  text: {
    color: 'black',
    fontSize: 16
  }
});
```

## Rendering Optimization

### 7\. Avoid calculations inside JSX

Process data before rendering for cleaner, more efficient code.

```
// Bad:
<Text>Output: {calculateSomething()}</Text>

// Good (value from store or pre-calculated):
<Text>Output: {preCalculatedValue}</Text>
```
```
// Example implementation:
const ProductList = ({ products }) => {
  // Calculate once before rendering
  const totalPrice = useMemo(() => 
    products.reduce((sum, p) => sum + p.price, 0), 
    [products]
  );

  return (
    <View>
      <Text>Total: ${totalPrice}</Text>
      {products.map(product => (
        <ProductItem key={product.id} product={product} />
      ))}
    </View>
  );
};
```

### 8\. Lazy load Bottom/Top tabs to render only when needed

Load tab content only when the user visits that tab.

```
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const Tab = createBottomTabNavigator();

export default function AppTabs() {
  return (
    <Tab.Navigator>
      <Tab.Screen name="Home" component={HomeScreen} />
      <Tab.Screen 
        name="Profile" 
        component={ProfileScreen}
        lazy={true} 
        lazyPlaceholder={() => <Loading />}
      />
      <Tab.Screen 
        name="Settings" 
        component={SettingsScreen}
        lazy={true}
      />
    </Tab.Navigator>
  );
}
```

### 9\. Don't render off-screen components in scroll views

Use a scroll handler to conditionally render components as they enter the viewport.

```
const LongScrollView = () => {
  const [visibleRange, setVisibleRange] = useState({ start: 0, end: 5 });

  const handleScroll = (event) => {
    const y = event.nativeEvent.contentOffset.y;
    const screenHeight = Dimensions.get('window').height;

    // Approximate which items are visible based on scroll position
    const startIndex = Math.max(0, Math.floor(y / ITEM_HEIGHT));
    const endIndex = Math.min(
      items.length - 1,
      Math.ceil((y + screenHeight) / ITEM_HEIGHT)
    );

    setVisibleRange({ start: startIndex, end: endIndex });
  };

  return (
    <ScrollView 
      onScroll={handleScroll}
      scrollEventThrottle={16}
    >
      {items.map((item, index) => (
        (index >= visibleRange.start - 2 && index <= visibleRange.end + 2) ? (
          <Item key={item.id} data={item} />
        ) : (
          <Placeholder key={item.id} height={ITEM_HEIGHT} />
        )
      ))}
    </ScrollView>
  );
};
```

### 10\. Use debounce to prevent extra renders & API calls

Delay processing until input stabilizes to avoid unnecessary operations.

```
import { debounce } from 'lodash';

const SearchBar = () => {
  const [query, setQuery] = useState('');

  const debouncedSearch = useCallback(
    debounce((searchTerm) => {
      performSearch(searchTerm);
    }, 300),
    []
  );

  const handleTextChange = (text) => {
    setQuery(text); // Update UI immediately
    debouncedSearch(text); // Delay API call
  };

  return (
    <TextInput
      value={query}
      onChangeText={handleTextChange}
      placeholder="Search..."
    />
  );
};
```

### 11\. Use InteractionManager to defer non-essential tasks

Prioritize animations and user interactions by deferring background work.

```
const ImageGallery = () => {
  const [imagesLoaded, setImagesLoaded] = useState(false);

  useEffect(() => {
    // Show placeholders immediately
    setPlaceholderImages();

    // Load high-quality images after animations complete
    InteractionManager.runAfterInteractions(() => {
      loadHighQualityImages().then(() => {
        setImagesLoaded(true);
      });
    });
  }, []);

  return (
    <View>
      {imagesLoaded ? <HighQualityGallery /> : <PlaceholderGallery />}
    </View>
  );
};
```

### 12\. Use Fragments instead of unnecessary View wrappers

Reduce component tree depth by eliminating unneeded container views.

```
// Bad - extra view in the component tree
const UserInfo = () => (
  <View>
    <Text>Name: {user.name}</Text>
    <Text>Email: {user.email}</Text>
  </View>
);

// Good - no extra node in the component tree
const UserInfo = () => (
  <>
    <Text>Name: {user.name}</Text>
    <Text>Email: {user.email}</Text>
  </>
);
```

### 13\. Optimize FlatList configuration for visible items

Fine-tune FlatList parameters for your specific use case.

```
<FlatList
  data={items}
  renderItem={renderItem}
  horizontal
  pagingEnabled
  maxToRenderPerBatch={5}
  initialNumToRender={2}
  windowSize={3}
  removeClippedSubviews={true}
  getItemLayout={(data, index) => ({
    length: ITEM_WIDTH,
    offset: ITEM_WIDTH * index,
    index
  })}
/>
```

For a horizontal FlatList with 20 items where only 2 are visible at a time and paging is enabled, these optimizations make a significant difference in scrolling performance.

## Performance & Efficiency

### 14\. Use FastImage

Replace the standard Image component for better loading, caching, and memory management.

```
import FastImage from 'react-native-fast-image';

const Avatar = ({ uri }) => (
  <FastImage
    source={{ 
      uri,
      priority: FastImage.priority.high,
      cache: FastImage.cacheControl.immutable
    }}
    style={styles.avatar}
    resizeMode={FastImage.resizeMode.cover}
  />
);
```

### 15\. Use FlashList instead of FlatList for better performance

FlashList offers significant performance improvements for long lists.

```
import { FlashList } from '@shopify/flash-list';

const ContactList = () => (
  <FlashList
    data={contacts}
    renderItem={({ item }) => <ContactItem contact={item} />}
    estimatedItemSize={75}
    keyExtractor={item => item.id}
  />
);
```

### 16\. Use Reanimated instead of Animated for animations

Reanimated runs animations on the UI thread for smoother performance.

```
import Animated, { 
  useSharedValue, 
  useAnimatedStyle, 
  withSpring 
} from 'react-native-reanimated';

const AnimatedButton = () => {
  const scale = useSharedValue(1);

  const animatedStyle = useAnimatedStyle(() => ({
    transform: [{ scale: scale.value }]
  }));

  const handlePress = () => {
    scale.value = withSpring(0.9, {}, () => {
      scale.value = withSpring(1);
    });
  };

  return (
    <Pressable onPress={handlePress}>
      <Animated.View style={[styles.button, animatedStyle]}>
        <Text>Press Me</Text>
      </Animated.View>
    </Pressable>
  );
};
```

### 17\. Optimize local images

Compress images before including them in your app to improve load time and prevent FPS drops.

```
// Before adding images to your project:
// 1. Use tools like TinyPNG, ImageOptim, or Squoosh
// 2. Choose appropriate resolutions for different device densities
// 3. Consider using WebP format for better compression

// Bad: original.png (250KB)
// Good: optimized.png (85KB)

const Logo = () => (
  <Image 
    source={require('./assets/optimized.png')}
    style={styles.logo}
  />
);
```

### 18\. Avoid racing conditions

When calling the same API multiple times, ensure you only use the latest response.

```
const SearchScreen = () => {
  const [results, setResults] = useState([]);
  const requestIdRef = useRef(0);

  const search = async (query) => {
    // Generate unique request ID
    const requestId = ++requestIdRef.current;

    try {
      const data = await api.search(query);

      // Only update if this is still the latest request
      if (requestId === requestIdRef.current) {
        setResults(data);
      }
    } catch (error) {
      console.error('Search failed:', error);
    }
  };

  return (
    <View>
      <SearchInput onSearch={search} />
      <ResultsList results={results} />
    </View>
  );
};
```

### 19\. Use Promise.allSettled() for parallel API calls

Run multiple API calls in parallel to reduce total wait time.

```
// Bad: (3 + 5 = 8 seconds)
const loadData = async () => {
  const userData = await getUserData(); // 3 seconds
  const postsData = await getPostsData(); // 5 seconds
  return { userData, postsData };
};

// Good: (5 seconds total)
const loadData = async () => {
  const [userResult, postsResult] = await Promise.allSettled([
    getUserData(),
    getPostsData()
  ]);

  return {
    userData: userResult.status === 'fulfilled' ? userResult.value : null,
    postsData: postsResult.status === 'fulfilled' ? postsResult.value : []
  };
};
```

### 20\. Reduce bundle size

Remove unnecessary dependencies and unused code to decrease app size and loading time.

```
// Bad - importing entire library
import moment from 'moment';

// Good - import only what you need
import { format } from 'date-fns';

// Bad - importing all icons
import { Icon } from 'react-native-elements';

// Good - import specific icons
import HomeIcon from 'path-to-icons/Home';
import ProfileIcon from 'path-to-icons/Profile';
```

### 21\. Reduce API over-fetching

Implement pagination and partial data loading to improve initial load times.

```
const ProductFeed = () => {
  const [products, setProducts] = useState([]);
  const [page, setPage] = useState(1);
  const [hasMore, setHasMore] = useState(true);

  const loadMore = async () => {
    if (!hasMore) return;

    const newProducts = await api.getProducts({
      page,
      limit: 20,
      fields: 'id,name,price,thumbnail' // Only fetch what you need
    });

    if (newProducts.length < 20) {
      setHasMore(false);
    }

    setProducts(prev => [...prev, ...newProducts]);
    setPage(prev => prev + 1);
  };

  return (
    <FlatList
      data={products}
      renderItem={renderProduct}
      onEndReached={loadMore}
      onEndReachedThreshold={0.5}
    />
  );
};
```

### 22\. Implement optimistic UI updates

Update the UI immediately on user action, then revert if the API call fails.

```
const FavoriteButton = ({ product, initialIsFavorite }) => {
  const [isFavorite, setIsFavorite] = useState(initialIsFavorite);

  const toggleFavorite = async () => {
    // Update UI immediately
    setIsFavorite(current => !current);

    try {
      // Attempt to update on server
      await api.setFavorite(product.id, !isFavorite);
    } catch (error) {
      // If fails, revert the UI change
      setIsFavorite(initialIsFavorite);
      Alert.alert('Failed to update favorite status');
    }
  };

  return (
    <TouchableOpacity onPress={toggleFavorite}>
      <Icon name={isFavorite ? 'heart' : 'heart-outline'} />
    </TouchableOpacity>
  );
};
```

### 23\. Show cached data immediately while fetching

Implement a stale-while-revalidate pattern to improve perceived performance.

```
const NewsFeed = () => {
  const [news, setNews] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const [isRefreshing, setIsRefreshing] = useState(false);

  useEffect(() => {
    // Immediately load cached data
    AsyncStorage.getItem('@news_cache').then(cached => {
      if (cached) {
        setNews(JSON.parse(cached));
        setIsLoading(false);
      }

      // Then fetch fresh data
      refreshData();
    });
  }, []);

  const refreshData = async () => {
    setIsRefreshing(true);
    try {
      const freshNews = await api.getNews();
      setNews(freshNews);
      await AsyncStorage.setItem('@news_cache', JSON.stringify(freshNews));
    } catch (error) {
      console.error('Failed to refresh news:', error);
    } finally {
      setIsLoading(false);
      setIsRefreshing(false);
    }
  };

  if (isLoading && news.length === 0) {
    return <LoadingIndicator />;
  }

  return (
    <FlatList
      data={news}
      renderItem={renderNewsItem}
      refreshing={isRefreshing}
      onRefresh={refreshData}
    />
  );
};
```

## Conclusion

These performance optimization techniques can dramatically improve your React Native app's speed, responsiveness, and user experience. Implement them strategically based on your specific app requirements and measurement results.

Remember: always measure performance before and after optimization to ensure your changes are having the intended effect. Premature optimization can sometimes add complexity without meaningful benefits.

By consistently applying these practices, you'll create React Native apps that not only work well but feel smooth and professional to your users.[Sentry](https://dev.to/sentry)Promoted

[![Sentry image](https://media2.dev.to/dynamic/image/width=775%2Cheight=%2Cfit=scale-down%2Cgravity=auto%2Cformat=auto/https%3A%2F%2Fimages.ctfassets.net%2Fem6l9zw4tzag%2F1GYxa0VJ4TOkpKyV4TaIur%2F34e4f6e2f1068894f9d0738008646289%2Fmcp-config.png%3Fw%3D1500%26h%3D1003%26q%3D50%26fm%3Dwebp)](https://blog.sentry.io/smarter-debugging-sentry-mcp-cursor/?utm_source=devto&utm_medium=paid-community&utm_campaign=smarter-debugging-mcp-cursor-blog&bb=240309)

## Smarter debugging with Sentry MCP and Cursor

No more copying and pasting error messages, logs, or trying to describe your distributed tracing setup or stack traces in chat. MCP can investigate real issues, understand their impact, and suggest fixes based on the actual production context.