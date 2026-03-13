A modern Android application demonstrating Clean Architecture, MVVM, and the latest Jetpack libraries. This project serves as a showcase for implementing robust local-remote data synchronization and persistent state management.

🛠 Project Configuration
1. Build SDK & Manifest
The project is configured with the latest Android SDK to utilize modern API features.

compileSdk: 36

targetSdk: 36

Permissions: Requires Internet access for Retrofit API calls.


<manifest xmlns:android="http://schemas.android.com/apk/res/android">
    <uses-permission android:name="android.permission.INTERNET"/>
    
    <application
        android:name=".MyApplication" 
        android:allowBackup="true"
        android:theme="@style/Theme.BookManager">
        </application>
</manifest>

2. Gradle Setup (Project Level)
Using KSP for efficient annotation processing and Hilt for Dependency Injection.

// File: build.gradle.kts (Project Level)


plugins {

    id("com.google.dagger.hilt.android") version "2.59.2" apply false
    id("com.google.devtools.ksp") version "2.2.10-2.0.2" apply false
    
}

3. Gradle Setup (App Level)
Comprehensive dependency list including Paging 3, Room, Retrofit, and Hilt.

// File: app/build.gradle.kts

plugins {

    id("com.android.application")
    id("org.jetbrains.kotlin.android")
    id("com.google.devtools.ksp")
    id("com.google.dagger.hilt.android")
    
}

android {

    compileSdk = 36
    // ... other configs
    
}

dependencies {

    // 📄 Pagination (Paging 3)
    
    implementation("androidx.paging:paging-runtime:3.4.2")
    implementation("androidx.paging:paging-compose:3.4.2")

    // 🌐 Network (Retrofit & OkHttp)
    implementation("com.squareup.retrofit2:retrofit:2.9.0")
    implementation("com.squareup.retrofit2:converter-gson:2.9.0")
    implementation("com.squareup.okhttp3:logging-interceptor:5.3.2")

    // 💉 Dependency Injection (Hilt)
    implementation("com.google.dagger:hilt-android:2.59.2")
    ksp("com.google.dagger:hilt-android-compiler:2.59.2")
    implementation("androidx.hilt:hilt-navigation-compose:1.3.0")

    // 🗄️ Local Database (Room)
    implementation("androidx.room:room-runtime:2.8.4")
    implementation("androidx.room:room-ktx:2.8.4")
    ksp("androidx.room:room-compiler:2.8.4")

    // 🔄 Lifecycle & Coroutines
    implementation("androidx.lifecycle:lifecycle-viewmodel-compose:2.10.0")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-core:1.10.2")
    implementation("org.jetbrains.kotlinx:kotlinx-coroutines-android:1.10.2")
    
}



// Ensure KSP works with Kotlin Source Sets

android.disallowKotlinSourceSets = false


🏛 Architecture Overview
MVVM & Clean Architecture

This app follows the Model-View-ViewModel pattern:

View (Jetpack Compose): A declarative UI that reacts to state changes.
ViewModel (Hilt-Injected): Manages UI state and business logic, leveraging viewModelScope for coroutines.
Repository: Acts as the Single Source of Truth, mediating between Room (local) and Retrofit (remote).

Key Features Implemented
Dependency Injection: Managed via Dagger Hilt for better testability and decoupled code.
Offline Support: Room Database ensures user data is accessible without an active internet connection.
Reactive UI: Utilizes Kotlin Flow to push real-time updates from the database to the Compose UI.
Efficient Processing: Using KSP instead of KAPT to significantly reduce build times.
Smooth Scrolling: Paging 3 integration for handling large datasets with minimal memory overhead.

🚀 How to Run

Clone the repository.
Ensure you have Android Studio Ladybug or newer.
Sync the project with Gradle files.
Run the app on an emulator or device running API 24 or higher.
