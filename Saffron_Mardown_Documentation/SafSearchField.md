# SafSearchField

## Overview

SafSearchField is a form component that provides search input functionality with autocomplete suggestions, filtering capabilities, and real-time search results. It supports various search modes, customizable suggestion rendering, keyboard navigation, and accessibility features for comprehensive search experiences.

## React API

### Props

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `string` | `''` | Current search query value |
| `defaultValue` | `string` | `''` | Default value (uncontrolled) |
| `placeholder` | `string` | `'Search...'` | Placeholder text |
| `suggestions` | `SearchSuggestion[]` | `[]` | Array of search suggestions |
| `results` | `SearchResult[]` | `[]` | Array of search results |
| `loading` | `boolean` | `false` | Show loading state |
| `disabled` | `boolean` | `false` | Disable the search field |
| `clearable` | `boolean` | `true` | Show clear button when has value |
| `searchDelay` | `number` | `300` | Debounce delay for search (ms) |
| `minSearchLength` | `number` | `1` | Minimum characters to trigger search |
| `maxSuggestions` | `number` | `10` | Maximum suggestions to show |
| `showSuggestions` | `boolean` | `true` | Show suggestions dropdown |
| `showResults` | `boolean` | `false` | Show results dropdown |
| `highlightMatch` | `boolean` | `true` | Highlight matching text in suggestions |
| `caseSensitive` | `boolean` | `false` | Case-sensitive search matching |
| `filterMode` | `'contains' \| 'startsWith' \| 'endsWith' \| 'exact'` | `'contains'` | Search filtering mode |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `variant` | `'default' \| 'outlined' \| 'filled'` | `'default'` | Visual style variant |
| `icon` | `ReactElement` | `<SearchIcon />` | Search icon |
| `iconPosition` | `'left' \| 'right'` | `'left'` | Icon position |
| `className` | `string` | - | Additional CSS classes |
| `style` | `object` | - | Inline styles |

### SearchSuggestion Interface

```typescript
interface SearchSuggestion {
  id: string | number;
  text: string;
  value: string;
  category?: string;
  icon?: ReactElement;
  description?: string;
  data?: any;
}

interface SearchResult {
  id: string | number;
  title: string;
  description?: string;
  url?: string;
  category?: string;
  icon?: ReactElement;
  thumbnail?: string;
  data?: any;
}
```

### Events

| Event | Type | Description |
|-------|------|-------------|
| `onChange` | `(value: string) => void` | Fired when input value changes |
| `onSearch` | `(query: string) => void` | Fired when search is triggered |
| `onSuggestionSelect` | `(suggestion: SearchSuggestion) => void` | Fired when suggestion is selected |
| `onResultSelect` | `(result: SearchResult) => void` | Fired when result is selected |
| `onClear` | `() => void` | Fired when search is cleared |
| `onFocus` | `(event: FocusEvent) => void` | Fired when field receives focus |
| `onBlur` | `(event: FocusEvent) => void` | Fired when field loses focus |

## Angular API

### Properties

| Property | Type | Default | Description |
|----------|------|---------|-------------|
| `value` | `string` | `''` | Current search query value |
| `placeholder` | `string` | `'Search...'` | Placeholder text |
| `suggestions` | `SearchSuggestion[]` | `[]` | Array of search suggestions |
| `results` | `SearchResult[]` | `[]` | Array of search results |
| `loading` | `boolean` | `false` | Show loading state |
| `disabled` | `boolean` | `false` | Disable the search field |
| `clearable` | `boolean` | `true` | Show clear button when has value |
| `searchDelay` | `number` | `300` | Debounce delay for search (ms) |
| `minSearchLength` | `number` | `1` | Minimum characters to trigger search |
| `maxSuggestions` | `number` | `10` | Maximum suggestions to show |
| `showSuggestions` | `boolean` | `true` | Show suggestions dropdown |
| `showResults` | `boolean` | `false` | Show results dropdown |
| `highlightMatch` | `boolean` | `true` | Highlight matching text in suggestions |
| `caseSensitive` | `boolean` | `false` | Case-sensitive search matching |
| `filterMode` | `'contains' \| 'startsWith' \| 'endsWith' \| 'exact'` | `'contains'` | Search filtering mode |
| `size` | `'small' \| 'medium' \| 'large'` | `'medium'` | Component size |
| `variant` | `'default' \| 'outlined' \| 'filled'` | `'default'` | Visual style variant |
| `iconPosition` | `'left' \| 'right'` | `'left'` | Icon position |

### Events

| Event | Type | Description |
|-------|------|-------------|
| `valueChange` | `EventEmitter<string>` | Fired when input value changes |
| `search` | `EventEmitter<string>` | Fired when search is triggered |
| `suggestionSelect` | `EventEmitter<SearchSuggestion>` | Fired when suggestion is selected |
| `resultSelect` | `EventEmitter<SearchResult>` | Fired when result is selected |
| `clear` | `EventEmitter<void>` | Fired when search is cleared |
| `fieldFocus` | `EventEmitter<FocusEvent>` | Fired when field receives focus |
| `fieldBlur` | `EventEmitter<FocusEvent>` | Fired when field loses focus |

## Usage Examples

### Basic Search Field

```typescript
// React
const BasicSearchField = ({ onSearch }) => {
  const [query, setQuery] = useState('');
  const [loading, setLoading] = useState(false);

  const handleSearch = async (searchQuery) => {
    if (searchQuery.trim().length === 0) return;
    
    setLoading(true);
    try {
      await onSearch(searchQuery);
    } finally {
      setLoading(false);
    }
  };

  return (
    <SafSearchField 
      value={query}
      onChange={setQuery}
      onSearch={handleSearch}
      loading={loading}
      placeholder="Search products..."
      clearable
      searchDelay={300}
      minSearchLength={2}
    />
  );
};
```

```html
<!-- Angular -->
<saf-search-field 
  [value]="query"
  [loading]="loading"
  placeholder="Search products..."
  [clearable]="true"
  [searchDelay]="300"
  [minSearchLength]="2"
  (valueChange)="onQueryChange($event)"
  (search)="onSearch($event)">
</saf-search-field>
```

### Search with Suggestions

```typescript
// React
const SearchWithSuggestions = ({ suggestions, onSearch }) => {
  const [query, setQuery] = useState('');
  const [filteredSuggestions, setFilteredSuggestions] = useState([]);

  useEffect(() => {
    if (query.length >= 1) {
      const filtered = suggestions
        .filter(suggestion => 
          suggestion.text.toLowerCase().includes(query.toLowerCase())
        )
        .slice(0, 8);
      setFilteredSuggestions(filtered);
    } else {
      setFilteredSuggestions([]);
    }
  }, [query, suggestions]);

  const handleSuggestionSelect = (suggestion) => {
    setQuery(suggestion.value);
    onSearch(suggestion.value);
  };

  const predefinedSuggestions = [
    {
      id: 1,
      text: 'Popular searches',
      value: 'popular',
      category: 'trending',
      icon: <SafIcon name="trending-up" />
    },
    {
      id: 2,
      text: 'Recent products',
      value: 'recent',
      category: 'history',
      icon: <SafIcon name="clock" />
    },
    {
      id: 3,
      text: 'Featured items',
      value: 'featured',
      category: 'featured',
      icon: <SafIcon name="star" />
    }
  ];

  return (
    <SafSearchField 
      value={query}
      onChange={setQuery}
      onSearch={onSearch}
      suggestions={query ? filteredSuggestions : predefinedSuggestions}
      onSuggestionSelect={handleSuggestionSelect}
      placeholder="Search for products, brands, or categories..."
      highlightMatch
      maxSuggestions={10}
    />
  );
};
```

### Advanced Search with Categories

```typescript
// React
const AdvancedSearchWithCategories = ({ 
  searchData, 
  onSearch, 
  onFilterChange 
}) => {
  const [query, setQuery] = useState('');
  const [selectedCategory, setSelectedCategory] = useState('all');
  const [suggestions, setSuggestions] = useState([]);

  const categories = [
    { id: 'all', name: 'All Categories', icon: 'search' },
    { id: 'products', name: 'Products', icon: 'package' },
    { id: 'articles', name: 'Articles', icon: 'file-text' },
    { id: 'users', name: 'Users', icon: 'users' },
    { id: 'documents', name: 'Documents', icon: 'folder' }
  ];

  const generateSuggestions = (searchQuery) => {
    if (searchQuery.length < 2) return [];

    const categorySuggestions = searchData
      .filter(item => {
        const matchesQuery = item.title.toLowerCase().includes(searchQuery.toLowerCase());
        const matchesCategory = selectedCategory === 'all' || item.category === selectedCategory;
        return matchesQuery && matchesCategory;
      })
      .map(item => ({
        id: item.id,
        text: item.title,
        value: item.title,
        category: item.category,
        icon: <SafIcon name={categories.find(c => c.id === item.category)?.icon || 'search'} />,
        description: item.description,
        data: item
      }))
      .slice(0, 8);

    return categorySuggestions;
  };

  useEffect(() => {
    setSuggestions(generateSuggestions(query));
  }, [query, selectedCategory, searchData]);

  const handleSearch = (searchQuery) => {
    onSearch(searchQuery, selectedCategory);
  };

  return (
    <div className="advanced-search">
      <div className="search-header">
        <SafSelect 
          value={selectedCategory}
          onChange={setSelectedCategory}
          className="category-selector"
        >
          {categories.map(category => (
            <SafOption key={category.id} value={category.id}>
              <SafIcon name={category.icon} />
              {category.name}
            </SafOption>
          ))}
        </SafSelect>
        
        <SafSearchField 
          value={query}
          onChange={setQuery}
          onSearch={handleSearch}
          suggestions={suggestions}
          onSuggestionSelect={(suggestion) => {
            setQuery(suggestion.value);
            handleSearch(suggestion.value);
          }}
          placeholder={`Search in ${categories.find(c => c.id === selectedCategory)?.name.toLowerCase()}...`}
          size="large"
          highlightMatch
        />
      </div>
    </div>
  );
};
```

### Search with Results Dropdown

```typescript
// React
const SearchWithResults = ({ searchAPI }) => {
  const [query, setQuery] = useState('');
  const [results, setResults] = useState([]);
  const [loading, setLoading] = useState(false);
  const [showResults, setShowResults] = useState(false);

  const handleSearch = async (searchQuery) => {
    if (searchQuery.trim().length < 2) {
      setResults([]);
      setShowResults(false);
      return;
    }

    setLoading(true);
    setShowResults(true);
    
    try {
      const searchResults = await searchAPI.search(searchQuery);
      setResults(searchResults.map(result => ({
        id: result.id,
        title: result.title,
        description: result.excerpt,
        url: result.url,
        category: result.type,
        icon: <SafIcon name={getIconForType(result.type)} />,
        thumbnail: result.thumbnail,
        data: result
      })));
    } catch (error) {
      console.error('Search failed:', error);
      setResults([]);
    } finally {
      setLoading(false);
    }
  };

  const handleResultSelect = (result) => {
    if (result.url) {
      window.open(result.url, '_blank');
    }
    setShowResults(false);
  };

  const getIconForType = (type) => {
    const iconMap = {
      article: 'file-text',
      product: 'package',
      user: 'user',
      video: 'video',
      image: 'image'
    };
    return iconMap[type] || 'file';
  };

  return (
    <div className="search-with-results">
      <SafSearchField 
        value={query}
        onChange={setQuery}
        onSearch={handleSearch}
        results={results}
        onResultSelect={handleResultSelect}
        loading={loading}
        showResults={showResults}
        placeholder="Search articles, products, and more..."
        searchDelay={400}
        minSearchLength={2}
      />
      
      {showResults && results.length === 0 && !loading && query.length >= 2 && (
        <div className="no-results">
          <SafEmptyState 
            icon={<SafIcon name="search" />}
            title="No results found"
            description={`No results for "${query}". Try different keywords.`}
          />
        </div>
      )}
    </div>
  );
};
```

### Filter-Integrated Search

```typescript
// React
const FilterIntegratedSearch = ({ 
  data, 
  filters, 
  onDataFilter, 
  onFilterChange 
}) => {
  const [searchQuery, setSearchQuery] = useState('');
  const [activeFilters, setActiveFilters] = useState({});
  const [suggestions, setSuggestions] = useState([]);

  const generateFilterSuggestions = (query) => {
    const filterSuggestions = [];
    
    // Add filter-based suggestions
    Object.entries(filters).forEach(([filterKey, filterConfig]) => {
      filterConfig.options.forEach(option => {
        if (option.label.toLowerCase().includes(query.toLowerCase())) {
          filterSuggestions.push({
            id: `filter-${filterKey}-${option.value}`,
            text: `${filterConfig.label}: ${option.label}`,
            value: option.label,
            category: 'filter',
            icon: <SafIcon name="filter" />,
            description: `Filter by ${filterConfig.label}`,
            data: { filterKey, filterValue: option.value }
          });
        }
      });
    });
    
    // Add content-based suggestions
    const contentSuggestions = data
      .filter(item => 
        item.title.toLowerCase().includes(query.toLowerCase()) ||
        item.tags?.some(tag => tag.toLowerCase().includes(query.toLowerCase()))
      )
      .map(item => ({
        id: `content-${item.id}`,
        text: item.title,
        value: item.title,
        category: 'content',
        icon: <SafIcon name="file" />,
        description: item.description,
        data: item
      }))
      .slice(0, 5);
    
    return [...filterSuggestions.slice(0, 3), ...contentSuggestions];
  };

  useEffect(() => {
    if (searchQuery.length >= 1) {
      setSuggestions(generateFilterSuggestions(searchQuery));
    } else {
      setSuggestions([]);
    }
  }, [searchQuery, data, filters]);

  const handleSuggestionSelect = (suggestion) => {
    if (suggestion.category === 'filter') {
      const { filterKey, filterValue } = suggestion.data;
      const newFilters = {
        ...activeFilters,
        [filterKey]: filterValue
      };
      setActiveFilters(newFilters);
      onFilterChange(newFilters);
      setSearchQuery('');
    } else {
      setSearchQuery(suggestion.value);
      handleSearch(suggestion.value);
    }
  };

  const handleSearch = (query) => {
    onDataFilter(query, activeFilters);
  };

  const clearFilter = (filterKey) => {
    const newFilters = { ...activeFilters };
    delete newFilters[filterKey];
    setActiveFilters(newFilters);
    onFilterChange(newFilters);
  };

  return (
    <div className="filter-integrated-search">
      <div className="search-bar">
        <SafSearchField 
          value={searchQuery}
          onChange={setSearchQuery}
          onSearch={handleSearch}
          suggestions={suggestions}
          onSuggestionSelect={handleSuggestionSelect}
          placeholder="Search or filter by criteria..."
          size="large"
        />
      </div>
      
      {Object.keys(activeFilters).length > 0 && (
        <div className="active-filters">
          <span className="filters-label">Active filters:</span>
          {Object.entries(activeFilters).map(([key, value]) => {
            const filterConfig = filters[key];
            const option = filterConfig.options.find(opt => opt.value === value);
            return (
              <SafFilterChip 
                key={key}
                label={`${filterConfig.label}: ${option?.label}`}
                onRemove={() => clearFilter(key)}
                removable
              />
            );
          })}
        </div>
      )}
    </div>
  );
};
```

### Contextual Search

```typescript
// React
const ContextualSearch = ({ context, searchAPI, onResultNavigate }) => {
  const [query, setQuery] = useState('');
  const [contextualSuggestions, setContextualSuggestions] = useState([]);
  const [loading, setLoading] = useState(false);

  const generateContextualSuggestions = async (searchQuery) => {
    if (searchQuery.length < 2) return [];

    setLoading(true);
    try {
      const suggestions = await searchAPI.getContextualSuggestions(
        searchQuery, 
        context
      );
      
      return suggestions.map(suggestion => ({
        id: suggestion.id,
        text: suggestion.text,
        value: suggestion.value,
        category: suggestion.context || 'general',
        icon: <SafIcon name={getContextIcon(suggestion.context)} />,
        description: suggestion.description,
        data: suggestion
      }));
    } catch (error) {
      console.error('Failed to fetch contextual suggestions:', error);
      return [];
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    const fetchSuggestions = async () => {
      const suggestions = await generateContextualSuggestions(query);
      setContextualSuggestions(suggestions);
    };

    if (query.length >= 2) {
      fetchSuggestions();
    } else {
      setContextualSuggestions([]);
    }
  }, [query, context]);

  const getContextIcon = (contextType) => {
    const iconMap = {
      'current-page': 'file',
      'recent-activity': 'clock',
      'related-content': 'link',
      'popular': 'trending-up',
      'personal': 'user'
    };
    return iconMap[contextType] || 'search';
  };

  const handleSearch = async (searchQuery) => {
    const results = await searchAPI.contextualSearch(searchQuery, context);
    onResultNavigate(results[0]); // Navigate to first result
  };

  return (
    <div className="contextual-search">
      <div className="context-info">
        <SafIcon name="info" size="small" />
        <span>Searching in {context.title}</span>
      </div>
      
      <SafSearchField 
        value={query}
        onChange={setQuery}
        onSearch={handleSearch}
        suggestions={contextualSuggestions}
        onSuggestionSelect={(suggestion) => {
          setQuery(suggestion.value);
          onResultNavigate(suggestion.data);
        }}
        loading={loading}
        placeholder={`Search in ${context.title}...`}
        icon={<SafIcon name={context.icon} />}
      />
    </div>
  );
};
```

### Mobile-Optimized Search

```typescript
// React
const MobileOptimizedSearch = ({ onSearch, suggestions }) => {
  const [query, setQuery] = useState('');
  const [isFocused, setIsFocused] = useState(false);
  const [isMobile, setIsMobile] = useState(window.innerWidth < 768);
  const [recentSearches, setRecentSearches] = useState([]);

  useEffect(() => {
    const handleResize = () => {
      setIsMobile(window.innerWidth < 768);
    };

    window.addEventListener('resize', handleResize);
    return () => window.removeEventListener('resize', handleResize);
  }, []);

  useEffect(() => {
    // Load recent searches from localStorage
    const recent = JSON.parse(localStorage.getItem('recentSearches') || '[]');
    setRecentSearches(recent.slice(0, 5));
  }, []);

  const handleSearch = (searchQuery) => {
    if (searchQuery.trim()) {
      // Save to recent searches
      const updatedRecent = [
        searchQuery,
        ...recentSearches.filter(s => s !== searchQuery)
      ].slice(0, 5);
      
      setRecentSearches(updatedRecent);
      localStorage.setItem('recentSearches', JSON.stringify(updatedRecent));
      
      onSearch(searchQuery);
    }
  };

  const clearRecentSearches = () => {
    setRecentSearches([]);
    localStorage.removeItem('recentSearches');
  };

  const mobileSuggestions = [
    ...recentSearches.map(search => ({
      id: `recent-${search}`,
      text: search,
      value: search,
      category: 'recent',
      icon: <SafIcon name="clock" />
    })),
    ...suggestions.slice(0, 5)
  ];

  return (
    <div className={`mobile-search ${isMobile ? 'mobile' : 'desktop'}`}>
      <SafSearchField 
        value={query}
        onChange={setQuery}
        onSearch={handleSearch}
        onFocus={() => setIsFocused(true)}
        onBlur={() => setTimeout(() => setIsFocused(false), 200)}
        suggestions={isFocused ? mobileSuggestions : []}
        placeholder="Search..."
        size={isMobile ? 'large' : 'medium'}
        variant="filled"
      />
      
      {isMobile && isFocused && (
        <div className="mobile-search-overlay">
          <div className="search-suggestions">
            {recentSearches.length > 0 && (
              <div className="recent-searches">
                <div className="section-header">
                  <span>Recent Searches</span>
                  <SafButton 
                    variant="ghost"
                    size="small"
                    onClick={clearRecentSearches}
                  >
                    Clear
                  </SafButton>
                </div>
                {recentSearches.map(search => (
                  <div 
                    key={search}
                    className="recent-search-item"
                    onClick={() => {
                      setQuery(search);
                      handleSearch(search);
                    }}
                  >
                    <SafIcon name="clock" size="small" />
                    <span>{search}</span>
                  </div>
                ))}
              </div>
            )}
          </div>
        </div>
      )}
    </div>
  );
};
```

### Voice Search Integration

```typescript
// React
const VoiceSearchField = ({ onSearch, onResults }) => {
  const [query, setQuery] = useState('');
  const [isListening, setIsListening] = useState(false);
  const [voiceSupported, setVoiceSupported] = useState(false);
  const recognitionRef = useRef(null);

  useEffect(() => {
    // Check for Web Speech API support
    if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
      setVoiceSupported(true);
      
      const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
      recognitionRef.current = new SpeechRecognition();
      
      recognitionRef.current.continuous = false;
      recognitionRef.current.interimResults = false;
      recognitionRef.current.lang = 'en-US';

      recognitionRef.current.onresult = (event) => {
        const transcript = event.results[0][0].transcript;
        setQuery(transcript);
        onSearch(transcript);
        setIsListening(false);
      };

      recognitionRef.current.onerror = (event) => {
        console.error('Speech recognition error:', event.error);
        setIsListening(false);
      };

      recognitionRef.current.onend = () => {
        setIsListening(false);
      };
    }

    return () => {
      if (recognitionRef.current) {
        recognitionRef.current.stop();
      }
    };
  }, [onSearch]);

  const startVoiceSearch = () => {
    if (recognitionRef.current && voiceSupported) {
      setIsListening(true);
      recognitionRef.current.start();
    }
  };

  const stopVoiceSearch = () => {
    if (recognitionRef.current) {
      recognitionRef.current.stop();
      setIsListening(false);
    }
  };

  return (
    <div className="voice-search-field">
      <SafSearchField 
        value={query}
        onChange={setQuery}
        onSearch={onSearch}
        placeholder="Search or speak your query..."
        icon={<SafIcon name="search" />}
        size="large"
      />
      
      {voiceSupported && (
        <SafButton 
          variant={isListening ? "danger" : "outline"}
          size="large"
          icon={<SafIcon name={isListening ? "mic-off" : "mic"} />}
          onClick={isListening ? stopVoiceSearch : startVoiceSearch}
          className="voice-button"
          aria-label={isListening ? "Stop voice search" : "Start voice search"}
        />
      )}
      
      {isListening && (
        <div className="listening-indicator">
          <SafIcon name="mic" className="pulse" />
          <span>Listening...</span>
        </div>
      )}
    </div>
  );
};
```

### Accessibility-Enhanced Search

```typescript
// React
const AccessibleSearchField = ({ 
  suggestions, 
  onSearch, 
  searchResults,
  label = "Search" 
}) => {
  const [query, setQuery] = useState('');
  const [selectedSuggestion, setSelectedSuggestion] = useState(-1);
  const [announcements, setAnnouncements] = useState('');
  const searchRef = useRef(null);

  const handleKeyDown = (event) => {
    switch (event.key) {
      case 'ArrowDown':
        event.preventDefault();
        const nextIndex = selectedSuggestion < suggestions.length - 1 
          ? selectedSuggestion + 1 
          : 0;
        setSelectedSuggestion(nextIndex);
        announceSelection(nextIndex);
        break;
        
      case 'ArrowUp':
        event.preventDefault();
        const prevIndex = selectedSuggestion > 0 
          ? selectedSuggestion - 1 
          : suggestions.length - 1;
        setSelectedSuggestion(prevIndex);
        announceSelection(prevIndex);
        break;
        
      case 'Enter':
        event.preventDefault();
        if (selectedSuggestion >= 0) {
          const suggestion = suggestions[selectedSuggestion];
          setQuery(suggestion.value);
          onSearch(suggestion.value);
        } else {
          onSearch(query);
        }
        break;
        
      case 'Escape':
        event.preventDefault();
        setSelectedSuggestion(-1);
        searchRef.current?.focus();
        break;
    }
  };

  const announceSelection = (index) => {
    if (index >= 0 && suggestions[index]) {
      const suggestion = suggestions[index];
      setAnnouncements(`${suggestion.text}, suggestion ${index + 1} of ${suggestions.length}`);
    }
  };

  const announceResults = (resultCount) => {
    const message = resultCount === 0 
      ? 'No search results found'
      : `${resultCount} search result${resultCount === 1 ? '' : 's'} found`;
    setAnnouncements(message);
  };

  useEffect(() => {
    if (searchResults) {
      announceResults(searchResults.length);
    }
  }, [searchResults]);

  return (
    <div className="accessible-search-field">
      <SafLabel htmlFor="accessible-search" className="search-label">
        {label}
      </SafLabel>
      
      <div 
        className="search-container"
        role="combobox"
        aria-expanded={suggestions.length > 0}
        aria-haspopup="listbox"
        aria-owns="search-suggestions"
      >
        <SafSearchField 
          ref={searchRef}
          id="accessible-search"
          value={query}
          onChange={setQuery}
          onSearch={onSearch}
          onKeyDown={handleKeyDown}
          suggestions={suggestions}
          placeholder="Enter search terms"
          aria-autocomplete="list"
          aria-activedescendant={
            selectedSuggestion >= 0 
              ? `suggestion-${selectedSuggestion}` 
              : undefined
          }
        />
        
        {suggestions.length > 0 && (
          <ul 
            id="search-suggestions"
            role="listbox"
            className="suggestions-list"
          >
            {suggestions.map((suggestion, index) => (
              <li
                key={suggestion.id}
                id={`suggestion-${index}`}
                role="option"
                aria-selected={selectedSuggestion === index}
                className={`suggestion-item ${selectedSuggestion === index ? 'selected' : ''}`}
                onClick={() => {
                  setQuery(suggestion.value);
                  onSearch(suggestion.value);
                }}
              >
                {suggestion.icon}
                <span>{suggestion.text}</span>
                {suggestion.description && (
                  <span className="suggestion-description">
                    {suggestion.description}
                  </span>
                )}
              </li>
            ))}
          </ul>
        )}
      </div>
      
      <div 
        aria-live="polite"
        aria-atomic="true"
        className="sr-only"
      >
        {announcements}
      </div>
      
      <div className="search-instructions sr-only">
        Use arrow keys to navigate suggestions, Enter to select, Escape to close.
      </div>
    </div>
  );
};
```

## Best Practices

### User Experience
- **Responsive Suggestions**: Provide relevant and timely search suggestions
- **Clear Feedback**: Show loading states and search progress clearly
- **Smart Defaults**: Use intelligent defaults for search behavior
- **Result Preview**: Show preview information for search results

### Performance
- **Debounced Input**: Use appropriate debounce delays to prevent excessive API calls
- **Caching**: Cache search results and suggestions for better performance
- **Lazy Loading**: Load suggestions and results incrementally
- **Request Cancellation**: Cancel previous requests when new searches start

### Accessibility
- **Keyboard Navigation**: Support arrow keys, Enter, and Escape for navigation
- **Screen Reader Support**: Provide clear announcements and context
- **Focus Management**: Maintain proper focus during interactions
- **ARIA Attributes**: Use comprehensive ARIA attributes for search functionality

### Search Quality
- **Fuzzy Matching**: Implement tolerance for typos and variations
- **Contextual Results**: Provide relevant results based on user context
- **Search History**: Remember and suggest previous successful searches
- **Advanced Filtering**: Allow users to refine and filter search results

## Accessibility Considerations

- Uses proper ARIA roles including `combobox`, `listbox`, and `option` patterns
- Supports comprehensive keyboard navigation for all search interactions
- Provides screen reader announcements for search results and suggestions
- Maintains proper focus management during suggestion navigation
- Includes descriptive labels and instructions for search functionality
- Supports high contrast mode and respects reduced motion preferences
- Uses semantic HTML structure for proper document outline

## Related Components

- **SafCombobox**: Dropdown selection component with search
- **SafAutocomplete**: Autocomplete input component
- **SafFilterChip**: Filter tag component for active filters
- **SafEmptyState**: Empty state for no search results

## Notes

- SafSearchField automatically handles debouncing and search optimization
- The component supports both client-side and server-side search implementations
- Suggestion rendering is highly customizable with support for icons and categories
- Voice search integration works in supported browsers
- Mobile optimizations provide touch-friendly search experiences
- The component integrates seamlessly with routing and navigation systems
- Advanced filtering capabilities support complex search scenarios
- Accessibility features ensure usability for all users regardless of abilities
