# Trade Me TCG Listing Assistant - Complete Specification

## Executive Summary
Web-based SaaS for NZ sellers to create high-quality Trade Me listings for Pokémon and MTG singles quickly.

## MVP Scope
- Single seller account support
- Card search (MTG & Pokémon)
- NZD price calculation  
- Draft generation
- Trade Me connection
- Manual confirmation before publishing

## Architecture Overview
- **Frontend:** Next.js + TypeScript
- **Backend:** Firebase Cloud Functions
- **Database:** Firebase Firestore
- **Auth:** Firebase Auth (Google sign-in)
- **API:** Trade Me OAuth 1.0a

## Key Components

### 1. Authentication & Security
- Firebase Auth with Google sign-in
- Trade Me OAuth 1.0a flow (server-side)
- Consumer secrets never reach client
- User data scoped by UID
- Sandbox environment first

### 2. Core Features

#### Card Search
- MTG and Pokémon card lookup
- Real-time pricing data
- Responsive list display
- Card image, set, and NZD price

#### Draft Builder
- Condition selection
- Quantity input
- Margin calculation
- Shipping template selection
- Draft save/edit functionality

#### Trade Me Integration
- OAuth flow handling
- Listing validation
- Photo upload support
- Manual publish confirmation
- Listing ID storage

### 3. Database Schema
- `users/{uid}/profile` - User settings and preferences
- `users/{uid}/drafts/{draftId}` - Listing drafts
- `users/{uid}/history/{listingId}` - Published listings
- `users/{uid}/trademe_tokens` - Trade Me OAuth tokens
- `system/fx_rates` - Exchange rates (read-only)
- `cards/cache` - Card metadata cache (read-only)

### 4. Backend Functions
- `initiateTrademeAuth` - Start OAuth flow
- `completeTrademeAuth` - Complete OAuth callback
- `searchCard` - Card search functionality
- `buildListingDraft` - Create draft listing
- `publishListingToTrademe` - Submit to Trade Me
- `getShippingTemplates` - Fetch shipping options
- `validateListingDraft` - Validate before submission

## Error Handling
- OAuth failure → Prompt reconnect
- Missing price → Manual price entry
- Photo upload failure → Allow listing without photo
- Validation failure → Show field-level errors
- Rate limit → Queue retry + notify user

## Development Roadmap

### Week 1: Foundation
- [ ] Scaffold Next.js app
- [ ] Set up Firebase project
- [ ] Implement authentication
- [ ] Add card search and pricing

### Week 2: Core Features  
- [ ] Build draft builder
- [ ] Implement Trade Me OAuth
- [ ] Add sandbox publish flow
- [ ] Store listing history

### Week 3: Polish & Test
- [ ] Add shipping templates
- [ ] Improve validation
- [ ] Photo handling
- [ ] User testing

## Security Considerations
- Trade Me secrets server-side only
- Firebase security rules for data access
- HTTPS for all API calls
- Input validation and sanitization
- Rate limiting implementation

## Next Steps
1. Register Trade Me sandbox application
2. Set up Firebase project structure
3. Create detailed UI mockups
4. Implement core authentication flow
5. Build card search integration

*Based on comprehensive Trade Me API research and best practices*
