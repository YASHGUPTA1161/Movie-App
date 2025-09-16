# WARP.md

This file provides guidance to WARP (warp.dev) when working with code in this repository.

## Project Overview

This is a React Native movie discovery app built with Expo, TypeScript, and Tailwind CSS (via NativeWind). The app fetches movie data from TMDB API and implements a popularity tracking system using Appwrite as the backend service.

## Development Commands

### Core Development
```bash
# Start the development server
npx expo start

# Platform-specific development
npx expo start --android    # Android emulator/device
npx expo start --ios        # iOS simulator/device  
npx expo start --web        # Web browser

# Install dependencies
npm install

# Reset project (removes example screens and components)
node ./scripts/reset-project.js
```

### Testing & Code Quality
```bash
# Run tests in watch mode
npm run test

# Run linting
npm run lint
```

### Environment Setup
Create a `.env` file in the root directory with:
```env
EXPO_PUBLIC_MOVIE_API_KEY=your_tmdb_api_key
EXPO_PUBLIC_APPWRITE_PROJECT_ID=your_appwrite_project_id
EXPO_PUBLIC_APPWRITE_DATABASE_ID=your_appwrite_database_id  
EXPO_PUBLIC_APPWRITE_COLLECTION_ID=your_appwrite_collection_id
```

## Architecture & Code Structure

### Navigation Architecture
- **Expo Router** with file-based routing system
- **Tab Navigation**: Bottom tabs for main sections (Home, Search, Save, Profile)
- **Stack Navigation**: Modal navigation for movie details
- **Route Structure**:
  - `app/(tabs)/` - Tab-based screens
  - `app/movie/[id].tsx` - Dynamic movie detail screen

### Data Layer Architecture
- **API Services** (`services/api.ts`): TMDB API integration for movie data
- **Backend Services** (`services/appwrite.ts`): Appwrite integration for popularity tracking
- **Custom Hooks** (`services/usefetch.ts`): Generic fetch hook with loading/error states
- **Type Definitions** (`interfaces/interfaces.d.ts`): TypeScript interfaces for Movie, MovieDetails, and TrendingMovie

### State Management Pattern
The app uses a custom `useFetch` hook pattern:
- Automatic data fetching with loading/error states
- Manual refetch capability
- Reset functionality for clearing state
- Generic typing for reusable data fetching

### Styling Architecture
- **NativeWind**: Tailwind CSS utilities for React Native
- **Custom Theme**: Extended Tailwind config with app-specific colors
- **Responsive Design**: Mobile-first approach with utility classes
- **Color Palette**:
  - Primary: `#030014` (Dark background)
  - Secondary: `#151312` 
  - Accent: `#AB8BFF` (Purple highlights)
  - Light variants: `#D6C7FF`, `#A8B5DB`, `#9CA4AB`

### Component Architecture
- **Reusable Components**: `MovieCard`, `SearchBar`, `TrendingCard`
- **Layout Components**: Custom tab icons with background highlights
- **Screen Components**: Tab screens and modal screens
- **Utility Components**: `MovieInfo` for consistent data display

### Key Features Implementation
- **Search with Debouncing**: 500ms delay to prevent API spam
- **Popularity Tracking**: Search terms tracked in Appwrite database with increment counters
- **Trending Algorithm**: Movies ranked by search frequency
- **Image Optimization**: TMDB image URLs with appropriate sizing
- **Error Handling**: Comprehensive error states and fallbacks

### Development Patterns
- **File-based routing** with Expo Router
- **Component composition** over inheritance
- **TypeScript-first** approach with strict typing
- **Custom hooks** for data fetching logic
- **Environment-based configuration** for API keys and endpoints
- **Utility-first CSS** with NativeWind

### API Integration
- **TMDB API**: Movie data, search, and detailed information
- **Appwrite**: Real-time database for tracking user interactions and generating trending data
- **Image CDN**: Optimized movie poster and backdrop delivery

### Platform Support
- **iOS**: Native iOS app via Expo
- **Android**: Native Android app via Expo  
- **Web**: Progressive web app support
- **New Architecture**: React Native's new architecture enabled

## Development Tips

### Working with Movie Data
- All movie data follows TMDB API structure
- Use TypeScript interfaces from `interfaces/interfaces.d.ts`
- Image URLs require TMDB base URL concatenation
- Handle missing poster paths with fallback images

### Styling Guidelines
- Use NativeWind utility classes over StyleSheet
- Follow the established color palette in `tailwind.config.js`
- Test UI on both iOS and Android for consistency
- Use responsive breakpoints for different screen sizes

### API Best Practices
- All API calls should use the `useFetch` hook
- Implement proper error handling and loading states
- Use environment variables for sensitive keys
- Implement debouncing for search functionality

### State Management
- Use the custom `useFetch` hook for server state
- Handle loading, error, and success states consistently
- Implement optimistic updates where appropriate
- Reset state when navigating between screens
