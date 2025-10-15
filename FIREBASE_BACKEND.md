# StyleSense Firebase Backend

A comprehensive Flutter fashion app with complete Firebase backend infrastructure, designed with SLT Mobitel corporate branding.

## 🏗️ Backend Architecture

### Core Services

#### 🔐 Authentication Service (`lib/services/auth_service.dart`)
- **Email/Password Authentication**: Secure user registration and login
- **Google Sign-In**: One-tap social authentication
- **Phone Authentication**: SMS-based verification
- **Password Reset**: Email-based password recovery
- **Profile Management**: User profile updates and photo management
- **Error Handling**: Comprehensive error management and user feedback

#### 🗄️ Firestore Service (`lib/services/firestore_service.dart`)
- **CRUD Operations**: Complete Create, Read, Update, Delete functionality
- **Real-time Streams**: Live data updates for feeds and user interactions
- **Pagination**: Efficient data loading with customizable page sizes
- **Search & Filtering**: Advanced search capabilities with multiple filters
- **Social Features**: Likes, saves, follows, and user interactions
- **Recommendations**: Personalized content recommendations
- **Analytics Integration**: User behavior tracking

#### 📊 Analytics Service (`lib/services/analytics_service.dart`)
- **Firebase Analytics**: Comprehensive user behavior tracking
- **Custom Events**: Fashion-specific event tracking
- **User Engagement**: Session tracking and user interaction analytics
- **Conversion Tracking**: Purchase intent and app performance metrics
- **Real-time Dashboards**: Live analytics data visualization

#### 🔔 Notification Service (`lib/services/notification_service.dart`)
- **Push Notifications**: Firebase Cloud Messaging integration
- **Local Notifications**: In-app notification management
- **Background Handling**: Notification processing when app is closed
- **Topic Subscriptions**: Category-based notification management
- **Social Notifications**: User interaction notifications

#### 🗂️ Database Initialization (`lib/services/database_init_service.dart`)
- **Reference Data**: Pre-populated categories, tags, brands, colors
- **Sample Data**: Demo content for development and testing
- **Batch Operations**: Efficient bulk data insertion
- **Validation**: Data integrity checks and initialization status

### Data Models

#### 👤 User Model (`lib/models/user_model.dart`)
```dart
class AppUser {
  // Core user information
  String uid, email, displayName;
  DateTime createdAt, lastLoginAt;
  
  // Fashion preferences
  List<String> styleTags, favoriteCategories;
  
  // Nested classes for organization
  UserPreferences preferences;
  UserProfile profile;
  UserStats stats;
  UserSubscription subscription;
  
  // Creator features
  bool isCreator, isVerified;
}
```

**Nested Classes:**
- `UserPreferences`: Notification and privacy settings
- `UserProfile`: Bio, location, social links
- `UserStats`: Followers, following, posts, engagement
- `NotificationSettings`: Granular notification controls
- `PrivacySettings`: Account privacy and visibility
- `UserSubscription`: Premium features and subscription status

#### 👗 Item Model (`lib/models/item_model.dart`)
```dart
class FashionItem {
  // Core item information
  String id, title, description, creatorId;
  List<String> imageUrls, styleTags, categories;
  
  // E-commerce features
  double? exactPrice;
  String priceRange, currency, brand;
  
  // Metadata and statistics
  ItemMetadata metadata;
  ItemStats stats;
  
  // Social features
  bool isActive, isFeatured;
}
```

**Supporting Classes:**
- `ItemStats`: Likes, views, shares, ratings
- `ItemMetadata`: SEO, moderation, seasonal data
- `Outfit`: Complete outfit compositions
- `Review`: User reviews and ratings system

## 🔒 Security Rules

### Firestore Security (`firestore.rules`)
- **Role-based Access Control**: Different permissions for users, creators, admins
- **Data Validation**: Server-side validation for all document fields
- **Privacy Protection**: User data protection and privacy controls
- **Content Moderation**: Automated content filtering and manual review workflows

### Storage Security (`storage.rules`)
- **Authenticated Uploads**: Only authenticated users can upload content
- **File Size Limits**: Maximum file size restrictions
- **File Type Validation**: Image format validation and security
- **User Ownership**: Users can only manage their own content

## 🎨 SLT Mobitel Branding

### Color Scheme
- **Primary**: `#E60012` (SLT Red)
- **Secondary**: `#1A1A1A` (Dark Gray)
- **Accent**: `#00A651` (SLT Green)

### Theme Implementation (`lib/theme/slt_theme.dart`)
- **Material 3 Design**: Modern Material Design implementation
- **Corporate Colors**: Consistent SLT branding throughout
- **Responsive Design**: Adaptive layouts for different screen sizes
- **Accessibility**: WCAG compliant color contrasts and font sizes

## 📱 App Configuration (`lib/config/app_config.dart`)

### Feature Flags
```dart
static const bool enableAnalytics = true;
static const bool enableNotifications = true;
static const bool enableSocialFeatures = true;
static const bool enableRecommendations = true;
```

### Environment Configuration
- **Development**: Debug features, extensive logging
- **Staging**: Production-like environment for testing
- **Production**: Optimized performance, minimal logging

### Performance Settings
- **Pagination**: 20 items per page (configurable)
- **Image Caching**: 7-day cache duration
- **Data Caching**: 30-minute cache for frequently accessed data

## 🚀 Getting Started

### Prerequisites
1. **Flutter**: Version 3.32.8 or higher
2. **Dart**: Version 3.8.1 or higher
3. **Firebase Project**: Create a new Firebase project
4. **Firebase CLI**: Install Firebase CLI tools

### Installation

1. **Clone the repository**
```bash
git clone <repository-url>
cd aiapp
```

2. **Install dependencies**
```bash
flutter pub get
```

3. **Configure Firebase**
```bash
# Install Firebase CLI
npm install -g firebase-tools

# Login to Firebase
firebase login

# Initialize Firebase in project
firebase init

# Generate Firebase configuration
flutterfire configure
```

4. **Deploy Security Rules**
```bash
# Deploy Firestore rules
firebase deploy --only firestore:rules

# Deploy Storage rules
firebase deploy --only storage:rules
```

5. **Initialize Database**
- The app will automatically initialize reference data on first run
- Sample data is created in debug mode for testing

### Firebase Project Setup

#### Enable Authentication
1. Go to Firebase Console → Authentication
2. Enable Sign-in methods:
   - Email/Password
   - Google
   - Phone (optional)

#### Configure Firestore
1. Go to Firebase Console → Firestore Database
2. Create database in production mode
3. Deploy security rules from `firestore.rules`

#### Configure Storage
1. Go to Firebase Console → Storage
2. Set up Cloud Storage bucket
3. Deploy security rules from `storage.rules`

#### Enable Analytics
1. Go to Firebase Console → Analytics
2. Enable Google Analytics for Firebase
3. Configure conversion events

#### Set up Cloud Messaging
1. Go to Firebase Console → Cloud Messaging
2. Configure FCM for push notifications
3. Add FCM service account keys

## 📊 Database Structure

### Collections

#### `users`
```
users/{userId}
├── uid: string
├── email: string
├── displayName: string
├── photoUrl: string
├── createdAt: timestamp
├── lastLoginAt: timestamp
├── styleTags: array
├── favoriteCategories: array
├── preferences: map
├── profile: map
├── stats: map
├── subscription: map
├── isCreator: boolean
└── isVerified: boolean
```

#### `items`
```
items/{itemId}
├── id: string
├── title: string
├── description: string
├── imageUrl: string
├── additionalImages: array
├── creatorId: string
├── creatorName: string
├── styleTags: array
├── categories: array
├── priceRange: string
├── exactPrice: number
├── currency: string
├── brand: string
├── color: string
├── sizes: array
├── stats: map
├── metadata: map
├── createdAt: timestamp
└── updatedAt: timestamp
```

#### Reference Collections
- `style_tags`: Available style categories
- `categories`: Fashion item categories
- `price_ranges`: Price range definitions
- `occasions`: Event/occasion types
- `seasons`: Seasonal categories
- `brands`: Fashion brand directory
- `colors`: Color palette
- `sizes`: Size definitions

### Subcollections
- `users/{userId}/notifications`: User notifications
- `users/{userId}/saved_items`: Saved/bookmarked items
- `users/{userId}/following`: Users being followed
- `items/{itemId}/reviews`: Item reviews and ratings
- `items/{itemId}/likes`: Like interactions

## 🔧 Configuration Files

### Environment Variables
Create `.env` file for sensitive configuration:
```
FIREBASE_API_KEY=your_api_key
FIREBASE_PROJECT_ID=your_project_id
FIREBASE_MESSAGING_SENDER_ID=your_sender_id
FIREBASE_APP_ID=your_app_id
```

### Firebase Configuration
- `firebase_options.dart`: Auto-generated Firebase configuration
- `android/app/google-services.json`: Android Firebase config
- `ios/Runner/GoogleService-Info.plist`: iOS Firebase config

## 📈 Analytics Events

### User Engagement
- `login`: User authentication events
- `sign_up`: New user registrations
- `screen_view`: Page/screen navigation
- `session_start`: App session tracking

### Fashion-Specific Events
- `item_view`: Fashion item views
- `item_like`: Item like interactions
- `item_share`: Item sharing actions
- `item_save`: Item bookmarking
- `search`: Search queries and results
- `filter_apply`: Filter usage analytics

### Creator Events
- `item_upload`: Creator content uploads
- `profile_view`: Creator profile views
- `follow_user`: User follow actions

## 🎯 Future Enhancements

### Planned Features
- **AI-Powered Recommendations**: Machine learning recommendations
- **Visual Search**: Image-based fashion search
- **Augmented Reality**: Virtual try-on experiences
- **E-commerce Integration**: In-app purchase capabilities
- **Social Commerce**: Creator monetization tools
- **Offline Mode**: Offline content caching

### Technical Improvements
- **GraphQL Integration**: Efficient data querying
- **Microservices Architecture**: Scalable backend services
- **CDN Integration**: Global content delivery
- **Advanced Caching**: Redis-based caching layer
- **Real-time Chat**: Creator-user communication

## 📞 Support

For technical support or questions:
- **Email**: support@stylesense.lk
- **Documentation**: [Firebase Documentation](https://firebase.google.com/docs)
- **Flutter Documentation**: [Flutter.dev](https://flutter.dev/docs)

## 📄 License

This project is part of the SLT Mobitel ecosystem and follows corporate licensing guidelines.

---

**StyleSense** - *Powered by SLT Mobitel Innovation*
