# Week 2: Authentication System

## Overview
Build a robust authentication system using Clerk and JWT for secure user authentication across the platform.

## Deliverables

### 1. User Registration
- Email/password registration form
- Form validation
- Password strength requirements
- Terms and conditions acceptance
- Account creation confirmation

### 2. Email Verification
- Verification email sending
- Email confirmation link
- Resend verification option
- Email confirmation page

### 3. Login/Logout
- Login form with email and password
- Session management
- Remember me functionality
- Logout functionality
- Session timeout

### 4. Password Reset
- Forgot password flow
- Password reset email
- Secure token verification
- Password update form
- Confirmation messaging

### 5. Social Login
- Google OAuth integration
- GitHub OAuth integration
- Account linking
- Profile auto-population

### 6. JWT Token Management
- Token generation on login
- Token refresh mechanism
- Token storage (secure)
- Token validation middleware
- Token expiration handling

## Technology Stack
- **Frontend:** Next.js + React + TailwindCSS
- **Backend:** Node.js + Express
- **Auth Provider:** Clerk
- **Database:** PostgreSQL
- **Token Management:** JWT (jsonwebtoken)
- **Password Hashing:** bcrypt

## Database Schema

### Users Table
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255),
  first_name VARCHAR(100),
  last_name VARCHAR(100),
  profile_picture_url TEXT,
  email_verified BOOLEAN DEFAULT FALSE,
  verified_at TIMESTAMP,
  is_active BOOLEAN DEFAULT TRUE,
  last_login TIMESTAMP,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  deleted_at TIMESTAMP
);

CREATE TABLE sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  refresh_token TEXT NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE password_resets (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  token VARCHAR(255) UNIQUE NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  used BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE oauth_accounts (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  provider VARCHAR(50) NOT NULL,
  provider_id VARCHAR(255) NOT NULL,
  email VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  UNIQUE(provider, provider_id)
);

CREATE TABLE email_verifications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  token VARCHAR(255) UNIQUE NOT NULL,
  expires_at TIMESTAMP NOT NULL,
  verified BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## API Endpoints

### Authentication Endpoints
```
POST   /api/auth/register          - User registration
POST   /api/auth/verify-email      - Verify email address
POST   /api/auth/resend-verification - Resend verification email
POST   /api/auth/login             - User login
POST   /api/auth/logout            - User logout
POST   /api/auth/refresh-token     - Refresh JWT token
POST   /api/auth/forgot-password   - Request password reset
POST   /api/auth/reset-password    - Reset password with token
POST   /api/auth/google            - Google OAuth login
POST   /api/auth/github            - GitHub OAuth login
GET    /api/auth/me                - Get current user info
```

## Implementation Steps

### Step 1: Setup Clerk
- [ ] Install Clerk SDK
- [ ] Configure Clerk environment variables
- [ ] Setup Clerk dashboard
- [ ] Configure social providers

### Step 2: Database Setup
- [ ] Create users table
- [ ] Create sessions table
- [ ] Create password_resets table
- [ ] Create oauth_accounts table
- [ ] Create email_verifications table
- [ ] Add indexes for performance

### Step 3: Backend Implementation
- [ ] Install required packages (bcrypt, jsonwebtoken, nodemailer)
- [ ] Create authentication middleware
- [ ] Implement registration endpoint
- [ ] Implement login endpoint
- [ ] Implement email verification
- [ ] Implement password reset
- [ ] Implement OAuth integration
- [ ] Implement JWT refresh logic
- [ ] Add error handling and validation

### Step 4: Frontend Implementation
- [ ] Create registration page
- [ ] Create login page
- [ ] Create password reset flow
- [ ] Create email verification page
- [ ] Integrate Clerk UI
- [ ] Add OAuth buttons
- [ ] Implement session management
- [ ] Add protected route guards

### Step 5: Security
- [ ] Implement CSRF protection
- [ ] Add rate limiting
- [ ] Implement secure password hashing
- [ ] Add JWT validation
- [ ] Implement CORS properly
- [ ] Add input validation
- [ ] Implement SQL injection prevention

### Step 6: Testing
- [ ] Unit tests for auth functions
- [ ] Integration tests for endpoints
- [ ] Test error scenarios
- [ ] Test edge cases
- [ ] Load testing

## Security Considerations

1. **Password Security**
   - Minimum 8 characters
   - Mix of uppercase, lowercase, numbers, symbols
   - Hash using bcrypt with salt rounds 10+
   - Never store plain passwords

2. **Token Security**
   - JWT signed with strong secret
   - Short expiration (15-30 minutes)
   - Refresh tokens with longer expiration
   - Secure storage (httpOnly cookies)

3. **Email Verification**
   - Unique verification tokens
   - Token expiration (24 hours)
   - Rate limit verification attempts

4. **Password Reset**
   - Unique reset tokens
   - Short expiration (1 hour)
   - Single use tokens
   - Verify email before reset

5. **Session Management**
   - Track active sessions
   - Allow session termination
   - Detect concurrent logins
   - Log authentication events

## Packages to Install

```bash
npm install clerk-sdk-node
npm install jsonwebtoken
npm install bcrypt
npm install nodemailer
npm install validator
npm install dotenv
npm install express-rate-limit
npm install cors
npm install helmet
npm install express-validator
```

## Testing Scenarios

- [ ] Register with valid email
- [ ] Register with invalid email
- [ ] Register with weak password
- [ ] Register with existing email
- [ ] Verify email with valid token
- [ ] Verify email with invalid token
- [ ] Login with correct credentials
- [ ] Login with incorrect credentials
- [ ] Login with unverified email
- [ ] Password reset flow
- [ ] OAuth login flow
- [ ] Token refresh
- [ ] Session timeout

## Commits Expected

```
[Week 2] Feature: Setup authentication database schema
[Week 2] Feature: Implement user registration endpoint
[Week 2] Feature: Add email verification system
[Week 2] Feature: Implement login and logout endpoints
[Week 2] Feature: Add password reset functionality
[Week 2] Feature: Integrate Clerk and OAuth
[Week 2] Feature: Add JWT token management
[Week 2] Feature: Create authentication frontend pages
[Week 2] Feature: Add security middleware and validation
[Week 2] Feature: Add authentication tests
```

## Success Criteria

✅ Users can register with email/password  
✅ Email verification works  
✅ Login/logout functions properly  
✅ Password reset works end-to-end  
✅ OAuth integration functional  
✅ JWT tokens generated and validated  
✅ Sessions properly managed  
✅ All security measures in place  
✅ Tests passing with 80%+ coverage  
✅ Documentation complete  

## Notes

- Use environment variables for sensitive data
- Implement proper error messages
- Log authentication events
- Monitor for suspicious activity
- Keep secrets out of version control
- Test on multiple browsers
- Consider rate limiting aggressively
