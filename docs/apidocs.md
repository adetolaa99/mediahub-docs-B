# Media Hub API Documentation

## Introduction

Welcome to the Media Hub API documentation. This API is designed to provide developers with a comprehensive set of tools to integrate with the Media Hub web application, enabling seamless access to a wide range of media content and functionalities.

### Purpose

The Media Hub API serves as the backbone for accessing and managing media content within the Media Hub web application. It facilitates the integration of media content from various sources, including user-generated content, licensed content, and third-party integrations.

### API Version

This documentation covers version 1.0 of the Media Hub API. It is important to note that the API may evolve over time, with new features, improvements, and changes to existing functionalities. Always refer to the latest version of this documentation for the most current information.

### Getting Started

To start using the Media Hub API, follow these steps:

1. **Register for an API Key**: Sign up for a Media Hub account and register for an API key. This key is required for authenticating your requests to the API.

2. **Explore the Documentation**: Use this documentation as your guide to understand the available endpoints and best practices for integrating with the Media Hub API.

3. **Test Your Integration**: Use tools like Postman or curl to test API requests and responses. This will help you understand how the API works and troubleshoot any issues that arise.

4. **Build Your Application**: With a solid understanding of the API and its capabilities, start building your application. Utilize the API to access and manage media content, personalize user experiences, and enhance your application's functionality.

5. **Support and Feedback**: We welcome feedback and questions from our users. If you encounter any issues or have suggestions for improving the API or this documentation, please contact our support team or submit your feedback through the Media Hub website.

## User Onboarding and Account Management

### Sign Up

The Sign Up endpoint allows new users to create an account on the Media Hub web app. This process includes providing an email address and setting a password or signing in to a specific social media account.

#### Request:

**Endpoint**: `/mediahub/signup`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "email": "user@exampleemail.com",
> "password": "userpassword"
> }

#### Response:

**Status Code**: `200 OK`

> {
> "message": "User successfully created",
> "user": {
> "id": 1,
> "email": "user@example.com"
> }
> }

#### Error Responses:

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid email or password.

- **Status Code**: `409 Conflict`
  - **Reason**: User already exists.

### Email Verification

After a user signs up, they need to verify their email address to activate their account. This process involves sending a verification email to the user's email address.

#### Request

**Endpoint**: `/mediahub/verify-email`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "email": "user@example.com", "verificationCode": "123456"
> }

#### Response

**Status Code**: `200 OK`

**Body**:

> {
> "message": "Email successfully verified",
> "user": {
> "id": 1,
> "email": "user@example.com", "isActive": true
> } }

#### Error Responses

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid email or verification code.

- **Status Code**: `404 Not Found`
  - **Reason**: User not found.

### Password Reset

If a user forgets their password, they can request a password reset. This process involves sending a password reset email to the user's email address.

#### Request

**Endpoint**: `/mediahub/reset-password`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "email": "user@example.com"
> }

#### Response:

**Status Code**: `200 OK`

**Body**

> {
> "message": "Password reset email sent",
> "user": {
> "id": 1,
> "email": "user@example.com"
> }
> }

#### Error Responses:

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid email.

- **Status Code**: `404 Not Found`
  - **Reason**: User not found.

## Media Integration and Content Aggregation

### Platform Integration

The Platform Integration endpoint allows users to connect their streaming platform accounts to Media Hub, enabling seamless access to their content across the platform.

#### Request

**Endpoint**: `/mediahub/content`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "platform": "Netflix",
> "accessToken": "access_token_from_streaming_platform"
> }

#### Response

**Status Code**: `200 OK`

> {
> "message": "Account successfully integrated",
> "user": {
> "id": 1,
> "email": "user@example.com"
> }
> }

#### Error Responses:

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid account or access token.

- **Status Code**: `409 Conflict`
  - **Reason**: Account already integrated.

### Search Functionality

The Search Functionality endpoint enables users to search for content across all connected platforms.

#### Request

**Endpoint**: `/mediahub/search`

**Method**: `GET`

**Headers**:

- `Content-Type: application/json`

**Query Parameters**:

- `query`: The search query.

#### Response

**Status Code**: `200 OK`

> {
> "results": [

    {
      "title": "Movie Title",
      "platform": "Netflix",
      "url": "https://www.netflix.com/title/123456"
    }

]
}

#### Error Responses

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid query.

- **Status Code**: `404 Not Found`
  - **Reason**: No results found.

### Playlist Creation

The Playlist Creation endpoint allows users to create and manage playlists that combine songs from different platforms.

#### Request

**Endpoint**: `/mediahub/song-playlists`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "name": "RnB gems",
> "description": "A playlist of my favorite RnB songs from various platforms." }

#### Response

**Status Code**: `201 Created`

> {
> "message": "Playlist successfully created",
> "playlist": {
> "id": 1,
> "name": "RnB gems",
> "description": "A playlist of my favorite RnB songs from various platforms."
> }
> }

#### Error Responses:

- **Status Code**: `400 Bad Request`

  - **Reason**: Invalid playlist name or description.

- **Status Code**: `409 Conflict`
  - **Reason**: Playlist already exists.

## User Dashboard and Consumption Tracking

The User Dashboard and Consumption Tracking features provide users with insights into their media consumption habits and personalized recommendations based on their preferences.

#### Total Watch Time

This endpoint allows users to view their total watch time for movies within the current month.

#### Request

**Endpoint**: `/mediahub/dashboard/watch-time`

**Method**: `GET`

**Headers**:

- `Content-Type: application/json`

#### Response:

**Status Code**: `200 OK`

> {
> "totalWatchTime": "10 hours",
> "message": "Total watch time for movies this month."
> }

#### Error Response:

- **Status Code**: `404 Not Found`
  - **Reason**: Total watch time not found or no data available.

#### Recommendations

This endpoint generates and returns personalized recommendations based on the user's favorite genres and viewing history.

#### Request

**Endpoint**: `/mediahub/recommendations`

**Method**: `GET`

**Headers**:

- `Content-Type: application/json`

#### Response

**Status Code**: `200 OK`

> {
> "recommendations":
> [ {
>
> > "title": "Recommended Movie Title"
> > "genre": "Action",
> > "url": "https://www.netflix.com/title/123456"
> > }, ... ],
> > "message": "Recommendations based on your favorite genres."
> > }

#### Error Response:

- **Status Code**: `400 Bad Request`
  - **Reason**: Invalid user ID or preferences not found.

#### Watch Goals

**Endpoint**: `/moviehub/goals`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "goal": "10 movies",
> "progress": "5 movies watched"
> }

#### Response

**Status Code**: `200 OK`

> {
> "message": "The goal of watching 10 movies this month is set and progress is being tracked."
> }

#### Error Response:

- **Status Code**: `400 Bad Request`
  - **Reason**: Invalid goal or progress data.

## Playlist Management and Social Sharing

Playlist Management and Social Sharing features allow users to enhance their media experience by managing their playlists and sharing them with others.

#### Request

**Endpoint**: `/api/playlist/manage`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "playlistId": "1",
> "songId": "song_123",
> "position": "2"
> }

#### Responses:

**Status Code**: `200 OK`

> {
> "message": "Song added to playlist and order rearranged."
> }

#### Error Response:

- **Status Code**: `404 Not Found`

  - **Reason**: Playlist or song not found

#### Share Playlist

This endpoint allows users to share their playlists on social media platforms, enhancing the discoverability of their curated content.

#### Request:

**Endpoint**: `/mediahub/playlist/share`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "playlistId": "1", "socialMediaPlatform": "Facebook"
> }

#### Response:

- **Status Code**: `200 OK`
  - **Body**:
    > {
    > "message": "Playlist shared on Facebook."
    > }

#### Error Response:

- **Status Code**: `400 Bad Request`
  - **Reason**: Invalid playlist ID or social media platform.

#### Collaborate on Playlist

This endpoint facilitates collaboration on playlists by allowing users to invite friends to contribute to their playlists.

#### Request:

**Endpoint**: `/mediahub/playlists/collaborate`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "playlistId": "1",
> "friendId": "friend_123"
> }

#### Response:

**Status Code**: `200 OK`

- **Body**:
  > {
  > "message": "Collaboration on playlist initiated."
  > }

#### Error Response:

- **Status Code**: `404 Not Found`
  - **Reason**: Playlist or friend not found.

## Offline Functionality and Download Options

The Offline Functionality and Download Options allow users to enjoy their media content without an internet connection and sync their offline changes when connected.

#### Download Playlist

This endpoint enables users to download their playlists for offline listening, enhancing their media consumption experience during periods without internet access.

#### Request:

**Endpoint**: `/mediahub/playlist/download`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "playlistId": "1"
> }

#### Response:

- **Status Code**: `200 OK`

  - **Body**:
    > {
    > "message": "Playlist downloaded for offline listening."
    > }

  #### Error Response:

- **Status Code**: `404 Not Found`
  - **Reason**: Playlist not found.

#### View Offline Content

This endpoint allows users to view the list of content available for offline viewing on their device.

#### Request:

**Endpoint**: `/mediahub/user/offline`

**Method**: `GET`

**Headers**:

- `Content-Type: application/json`

#### Response:

**Status Code**: `200 OK`

- **Body**:
  > {
  > "offlineContent": [ {
      "title": "Offline Movie Title", "genre": "Action",
      "url": "https://www.netflix.com/title/123456"
      }, ... ],
      "message": "View available offline content on your device." }

#### Error Response:

- **Status Code**: `400 Bad Request`
  - **Reason**: Device not found or no offline content available.

#### Sync Offline Changes

This endpoint enables users to sync their offline changes, such as song additions and rearrangements, when they reconnect to the internet.

#### Request:

**Endpoint**: `/mediahub/user/sync`

**Method**: `POST`

**Headers**:

- `Content-Type: application/json`

**Body**:

> {
> "offlineChanges": [ {
>
> > "playlistId": "1",
> > "songId": "song_123",
> > "position": "2" }, ...
> > ] }

#### Response:

**Status Code**: `200 OK`

- **Body**:
  > {
  > "message": "Offline changes synced when connected to the internet."
  > }

#### Error Response:

- **Status Code**: `400 Bad Request`
  - **Reason**: Could not save data offline.
