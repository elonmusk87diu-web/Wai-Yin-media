# Wai-Yin-media
社交媒體

<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Wai Yin Media</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css" rel="stylesheet">
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    colors: {
                        primary: '#5D5CDE',
                        'primary-dark': '#4C4BC9',
                    }
                }
            }
        }
    </script>
</head>
<body class="bg-white dark:bg-gray-900 text-gray-900 dark:text-white transition-colors duration-300">
    <!-- Navigation -->
    <nav class="bg-white dark:bg-gray-800 border-b border-gray-200 dark:border-gray-700 sticky top-0 z-50">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex justify-between h-16">
                <div class="flex items-center">
                    <div class="flex-shrink-0">
                        <h1 class="text-2xl font-bold text-primary">Wai Yin</h1>
                    </div>
                    <div class="hidden md:ml-6 md:flex md:space-x-8">
                        <a href="#" class="nav-link active" data-tab="home">
                            <i class="fas fa-home mr-2"></i>主頁
                        </a>
                        <a href="#" class="nav-link" data-tab="discover">
                            <i class="fas fa-compass mr-2"></i>探索
                        </a>
                                 <i class="fas fa-compass mr-2"></i>認識林湋然
                        </a>
                        <a href="#" class="nav-link" data-tab="profile">
                            <i class="fas fa-user mr-2"></i>個人資料
                        </a>
                        <a href="#" class="nav-link" data-tab="notifications">
                            <i class="fas fa-bell mr-2"></i>通知
                            <span id="notification-badge" class="bg-red-500 text-white text-xs rounded-full px-2 py-1 ml-1">0</span>
                        </a>
                    </div>
                </div>
                <div class="flex items-center space-x-4">
                    <button id="auth-btn" class="bg-primary hover:bg-primary-dark text-white px-4 py-2 rounded-lg transition-colors">
                        登入
                    </button>
                    <div id="user-menu" class="hidden relative">
                        <button id="user-menu-btn" class="flex items-center space-x-2 text-sm bg-gray-200 dark:bg-gray-700 rounded-full p-2 hover:bg-gray-300 dark:hover:bg-gray-600 transition-colors">
                            <img id="user-avatar" class="w-8 h-8 rounded-full" src="" alt="Avatar">
                            <span id="user-name">用戶</span>
                        </button>
                        <div id="user-dropdown" class="hidden absolute right-0 mt-2 w-48 bg-white dark:bg-gray-800 rounded-md shadow-lg py-1 z-50">
                            <button id="logout-btn" class="block px-4 py-2 text-sm text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700 w-full text-left">
                                <i class="fas fa-sign-out-alt mr-2"></i>登出
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </nav>

    <!-- Main Content -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
        <!-- Login/Register Modal -->
        <div id="auth-modal" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg max-w-md w-full mx-4">
                <div class="flex justify-between items-center mb-6">
                    <h2 id="auth-title" class="text-2xl font-bold">登入</h2>
                    <button id="close-modal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <form id="auth-form">
                    <div id="register-fields" class="hidden">
                        <div class="mb-4">
                            <label class="block text-sm font-medium mb-2">用戶名</label>
                            <input type="text" id="username" class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary text-base bg-white dark:bg-gray-700" placeholder="請輸入用戶名">
                        </div>
                    </div>
                    <div class="mb-4">
                        <label class="block text-sm font-medium mb-2">電子郵件</label>
                        <input type="email" id="email" class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary text-base bg-white dark:bg-gray-700" placeholder="請輸入電子郵件">
                    </div>
                    <div class="mb-6">
                        <label class="block text-sm font-medium mb-2">密碼</label>
                        <input type="password" id="password" class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary text-base bg-white dark:bg-gray-700" placeholder="請輸入密碼">
                    </div>
                    <button type="submit" class="w-full bg-primary hover:bg-primary-dark text-white py-2 rounded-lg transition-colors">
                        <span id="auth-submit-text">登入</span>
                    </button>
                </form>
                <div class="mt-4 text-center">
                    <button id="toggle-auth" class="text-primary hover:underline">
                        <span id="toggle-auth-text">還沒有帳戶？註冊</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- Profile Edit Modal -->
        <div id="profile-edit-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg max-w-md w-full mx-4">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold">編輯個人資料</h2>
                    <button id="close-profile-modal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <form id="profile-edit-form">
                    <div class="mb-4">
                        <label class="block text-sm font-medium mb-2">用戶名</label>
                        <input type="text" id="profile-username" class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary text-base bg-white dark:bg-gray-700">
                    </div>
                    <div class="mb-4">
                        <label class="block text-sm font-medium mb-2">個人簡介</label>
                        <textarea id="profile-bio" class="w-full px-3 py-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary text-base bg-white dark:bg-gray-700 resize-none" rows="3"></textarea>
                    </div>
                    <button type="submit" class="w-full bg-primary hover:bg-primary-dark text-white py-2 rounded-lg transition-colors">
                        儲存變更
                    </button>
                </form>
            </div>
        </div>

        <!-- User Profile Modal -->
        <div id="user-profile-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold">用戶資料</h2>
                    <button id="close-user-profile-modal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <div id="user-profile-content">
                    <!-- 動態生成內容 -->
                </div>
            </div>
        </div>

        <!-- Comment Modal -->
        <div id="comment-modal" class="hidden fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
            <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg max-w-2xl w-full mx-4 max-h-[90vh] overflow-y-auto">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-bold">評論</h2>
                    <button id="close-comment-modal" class="text-gray-500 hover:text-gray-700">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
                <div id="comment-content">
                    <!-- 動態生成內容 -->
                </div>
            </div>
        </div>

        <!-- Home Tab -->
        <div id="home-tab" class="tab-content">
            <div class="grid grid-cols-1 lg:grid-cols-3 gap-8">
                <!-- Left Sidebar -->
                <div class="lg:col-span-1">
                    <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 mb-6">
                        <h3 class="text-lg font-bold mb-4">個人資訊</h3>
                        <div class="flex items-center space-x-3 mb-4">
                            <img id="sidebar-avatar" class="w-12 h-12 rounded-full" src="" alt="Avatar">
                            <div>
                                <p id="sidebar-username" class="font-semibold">請先登入</p>
                                <p id="sidebar-handle" class="text-sm text-gray-500">@guest</p>
                            </div>
                        </div>
                        <div class="grid grid-cols-3 gap-4 text-center">
                            <div>
                                <p id="sidebar-posts" class="font-bold text-lg">0</p>
                                <p class="text-sm text-gray-500">發文</p>
                            </div>
                            <div>
                                <p id="sidebar-following" class="font-bold text-lg">0</p>
                                <p class="text-sm text-gray-500">關注</p>
                            </div>
                            <div>
                                <p id="sidebar-followers" class="font-bold text-lg">0</p>
                                <p class="text-sm text-gray-500">粉絲</p>
                            </div>
                        </div>
                    </div>

                    <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6">
                        <h3 class="text-lg font-bold mb-4">熱門標籤</h3>
                        <div id="trending-tags" class="space-y-2">
                            <!-- 動態生成 -->
                        </div>
                    </div>
                </div>

                <!-- Main Feed -->
                <div class="lg:col-span-2">
                    <!-- Create Post -->
                    <div id="create-post-section" class="hidden bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 mb-6">
                        <div class="flex space-x-4">
                            <img id="create-post-avatar" class="w-10 h-10 rounded-full" src="" alt="Avatar">
                            <div class="flex-1">
                                <textarea id="post-content" placeholder="分享你的想法..." class="w-full p-3 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary resize-none text-base bg-white dark:bg-gray-700" rows="3"></textarea>
                                <div class="flex justify-between items-center mt-4">
                                    <div class="flex space-x-4">
                                        <input type="file" id="image-upload" accept="image/*" class="hidden">
                                        <button id="image-btn" class="text-gray-500 hover:text-primary transition-colors">
                                            <i class="fas fa-image"></i>
                                        </button>
                                        <button id="hashtag-btn" class="text-gray-500 hover:text-primary transition-colors">
                                            <i class="fas fa-hashtag"></i>
                                        </button>
                                    </div>
                                    <button id="post-btn" class="bg-primary hover:bg-primary-dark text-white px-6 py-2 rounded-lg transition-colors">
                                        發布
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Feed Filter -->
                    <div id="feed-filter" class="hidden bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4 mb-6">
                        <div class="flex space-x-4">
                            <button id="feed-all" class="px-4 py-2 rounded-lg bg-primary text-white">所有貼文</button>
                            <button id="feed-following" class="px-4 py-2 rounded-lg bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300">關注的人</button>
                        </div>
                    </div>

                    <!-- Posts Feed -->
                    <div id="posts-container" class="space-y-6">
                        <!-- 動態生成貼文 -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Discover Tab -->
        <div id="discover-tab" class="tab-content hidden">
            <div class="max-w-4xl mx-auto">
                <h2 class="text-2xl font-bold mb-6">探索用戶</h2>
                <div id="discover-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- 動態生成用戶卡片 -->
                </div>
            </div>
        </div>

        <!-- Profile Tab -->
        <div id="profile-tab" class="tab-content hidden">
            <div class="max-w-4xl mx-auto">
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-8">
                    <div class="flex flex-col md:flex-row items-center md:items-start space-y-4 md:space-y-0 md:space-x-8">
                        <img id="profile-avatar" class="w-32 h-32 rounded-full" src="" alt="Profile Avatar">
                        <div class="flex-1 text-center md:text-left">
                            <h2 id="profile-name" class="text-3xl font-bold mb-2">請先登入</h2>
                            <p id="profile-handle" class="text-gray-500 mb-4">@guest</p>
                            <p id="profile-bio" class="mb-6">請登入後編輯您的個人簡介</p>
                            <div class="flex justify-center md:justify-start space-x-6 mb-6">
                                <div class="text-center">
                                    <p id="profile-posts-count" class="font-bold text-xl">0</p>
                                    <p class="text-gray-500">發文</p>
                                </div>
                                <div class="text-center">
                                    <p id="profile-following-count" class="font-bold text-xl">0</p>
                                    <p class="text-gray-500">關注</p>
                                </div>
                                <div class="text-center">
                                    <p id="profile-followers-count" class="font-bold text-xl">0</p>
                                    <p class="text-gray-500">粉絲</p>
                                </div>
                            </div>
                            <button id="edit-profile-btn" class="hidden bg-primary hover:bg-primary-dark text-white px-6 py-2 rounded-lg transition-colors">
                                編輯個人資料
                            </button>
                        </div>
                    </div>
                </div>

                <!-- User Posts -->
                <div class="mt-8">
                    <h3 class="text-xl font-bold mb-6">我的發文</h3>
                    <div id="user-posts-container" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                        <!-- 動態生成用戶貼文 -->
                    </div>
                </div>
            </div>
        </div>

        <!-- Notifications Tab -->
        <div id="notifications-tab" class="tab-content hidden">
            <div class="max-w-4xl mx-auto">
                <h2 class="text-2xl font-bold mb-6">通知</h2>
                <div id="notifications-container" class="bg-white dark:bg-gray-800 rounded-lg shadow-lg divide-y divide-gray-200 dark:divide-gray-700">
                    <!-- 動態生成通知 -->
                </div>
            </div>
        </div>
    </div>

    <!-- Mobile Bottom Navigation -->
    <nav class="md:hidden fixed bottom-0 left-0 right-0 bg-white dark:bg-gray-800 border-t border-gray-200 dark:border-gray-700">
        <div class="flex justify-around py-2">
            <button class="nav-link-mobile active" data-tab="home">
                <i class="fas fa-home text-xl"></i>
            </button>
            <button class="nav-link-mobile" data-tab="discover">
                <i class="fas fa-compass text-xl"></i>
            </button>
            <button class="nav-link-mobile" data-tab="profile">
                <i class="fas fa-user text-xl"></i>
            </button>
            <button class="nav-link-mobile" data-tab="notifications">
                <i class="fas fa-bell text-xl"></i>
            </button>
        </div>
    </nav>

    <script>
        // 應用程式狀態管理
        class AppState {
            constructor() {
                this.currentUser = null;
                this.users = new Map();
                this.posts = [];
                this.comments = new Map(); // postId -> comments array
                this.notifications = [];
                this.isLoggedIn = false;
                this.nextUserId = 1;
                this.nextPostId = 1;
                this.nextCommentId = 1;
                this.nextNotificationId = 1;
                this.hashtags = new Map();
                this.feedFilter = 'all'; // 'all' or 'following'
                
                this.initializeApp();
            }

            initializeApp() {
                // 創建示例用戶
                this.createSampleUsers();
                // 創建示例貼文
                this.createSamplePosts();
                // 創建示例評論
                this.createSampleComments();
                // 創建示例通知
                this.createSampleNotifications();
                // 更新熱門標籤
                this.updateTrendingTags();
            }

            createSampleUsers() {
                const sampleUsers = [
                    {
                        username: '林小雅',
                        email: 'alice@example.com',
                        bio: '集團董事長',
                        avatar: 'https://ui-avatars.com/api/?name=林湋然&background=FF6B6B&color=fff',
                        followers: new Set([3000000000000]),
                        following: new Set([3000000000]),
                        posts: 24
                    },
                    {
                        username: '王大明',
                        email: 'bob@example.com',
                        bio: '程式設計師 | 咖啡愛好者 ☕ | 喜歡分享技術心得',
                        avatar: 'https://ui-avatars.com/api/?name=王大明&background=4ECDC4&color=fff',
                        followers: new Set([1, 3]),
                        following: new Set([1, 3]),
                        posts: 18
                    },
                    {
                        username: '陳美麗',
                        email: 'charlie@example.com',
                        bio: '美食評論家 🍜 | 分享生活中的美好時光',
                        avatar: 'https://ui-avatars.com/api/?name=陳美麗&background=45B7D1&color=fff',
                        followers: new Set([2]),
                        following: new Set([1, 2]),
                        posts: 32
                    },
                    {
                        username: '李小花',
                        email: 'diana@example.com',
                        bio: '音樂愛好者 🎵 | 喜歡分享日常生活',
                        avatar: 'https://ui-avatars.com/api/?name=李小花&background=96CEB4&color=fff',
                        followers: new Set(),
                        following: new Set([1]),
                        posts: 12
                    }
                ];

                sampleUsers.forEach(userData => {
                    const user = this.createUser(userData.username, userData.email, '123456', userData.bio);
                    user.avatar = userData.avatar;
                    user.followers = userData.followers;
                    user.following = userData.following;
                    user.postsCount = userData.posts;
                });
            }

            createSamplePosts() {
                const samplePosts = [
                    {
                        userId: 1,
                        content: '今天天氣真好！和朋友們一起去了海邊，拍了很多美照 📸 大家週末愉快！ #攝影 #海邊 #週末',
                        timestamp: Date.now() - 2 * 60 * 60 * 1000,
                        likes: 24,
                        shares: 3,
                        image: 'https://picsum.photos/600/400?random=1'
                    },
                    {
                        userId: 2,
                        content: '剛完成了一個新的網站專案！使用了最新的前端技術，效果非常棒 💻 分享給大家一些開發心得... #程式設計 #前端開發 #技術分享',
                        timestamp: Date.now() - 5 * 60 * 60 * 1000,
                        likes: 15,
                        shares: 5
                    },
                    {
                        userId: 3,
                        content: '今天發現了一家超棒的拉麵店！湯頭濃郁，麵條Q彈，真的是人間美味 🍜 推薦給所有美食愛好者！ #美食 #拉麵 #推薦',
                        timestamp: Date.now() - 8 * 60 * 60 * 1000,
                        likes: 31,
                        shares: 2,
                        image: 'https://picsum.photos/600/400?random=2'
                    },
                    {
                        userId: 1,
                        content: '分享一些攝影小技巧：黃金時段拍照真的差很多！日出日落的光線最美了 🌅 #攝影技巧 #黃金時段',
                        timestamp: Date.now() - 24 * 60 * 60 * 1000,
                        likes: 42,
                        shares: 8
                    },
                    {
                        userId: 4,
                        content: '今天練習了新的歌曲，終於彈出來了！音樂真的能治癒心靈 🎸 #音樂 #吉他 #練習',
                        timestamp: Date.now() - 12 * 60 * 60 * 1000,
                        likes: 18,
                        shares: 1
                    }
                ];

                samplePosts.forEach(postData => {
                    const post = this.createPost(postData.userId, postData.content, postData.image);
                    post.timestamp = postData.timestamp;
                    post.likes = postData.likes;
                    post.shares = postData.shares;
                    post.likedBy = new Set();
                });
            }

            createSampleComments() {
                const sampleComments = [
                    { postId: 1, userId: 2, content: '照片拍得真好看！', timestamp: Date.now() - 1 * 60 * 60 * 1000 },
                    { postId: 1, userId: 3, content: '海邊真的很美，下次我也想去！', timestamp: Date.now() - 30 * 60 * 1000 },
                    { postId: 2, userId: 1, content: '技術分享很棒，學到了很多！', timestamp: Date.now() - 4 * 60 * 60 * 1000 },
                    { postId: 3, userId: 2, content: '這家拉麵店在哪裡？我也想去試試！', timestamp: Date.now() - 6 * 60 * 60 * 1000 }
                ];

                sampleComments.forEach(commentData => {
                    this.addComment(commentData.postId, commentData.userId, commentData.content, commentData.timestamp);
                });
            }

            createSampleNotifications() {
                const notifications = [
                    {
                        type: 'like',
                        fromUserId: 2,
                        message: '喜歡了你的發文',
                        timestamp: Date.now() - 2 * 60 * 60 * 1000
                    },
                    {
                        type: 'follow',
                        fromUserId: 3,
                        message: '開始關注你',
                        timestamp: Date.now() - 5 * 60 * 60 * 1000
                    },
                    {
                        type: 'comment',
                        fromUserId: 1,
                        message: '評論了你的發文：「很棒的分享！」',
                        timestamp: Date.now() - 24 * 60 * 60 * 1000
                    }
                ];

                notifications.forEach(notif => {
                    this.addNotification(notif.type, notif.fromUserId, notif.message, notif.timestamp);
                });
            }

            createUser(username, email, password, bio = '') {
                const user = {
                    id: this.nextUserId++,
                    username,
                    email,
                    password,
                    bio,
                    avatar: `https://ui-avatars.com/api/?name=${encodeURIComponent(username)}&background=5D5CDE&color=fff`,
                    followers: new Set(),
                    following: new Set(),
                    postsCount: 0,
                    joinDate: new Date()
                };
                this.users.set(user.id, user);
                return user;
            }

            login(email, password) {
                for (let user of this.users.values()) {
                    if (user.email === email && user.password === password) {
                        this.currentUser = user;
                        this.isLoggedIn = true;
                        return { success: true, user };
                    }
                }
                return { success: false, message: '電子郵件或密碼錯誤' };
            }

            register(username, email, password) {
                for (let user of this.users.values()) {
                    if (user.email === email) {
                        return { success: false, message: '電子郵件已被使用' };
                    }
                }
                
                const user = this.createUser(username, email, password);
                this.currentUser = user;
                this.isLoggedIn = true;
                return { success: true, user };
            }

            logout() {
                this.currentUser = null;
                this.isLoggedIn = false;
            }

            createPost(userId, content, image = null) {
                const post = {
                    id: this.nextPostId++,
                    userId,
                    content,
                    image,
                    timestamp: Date.now(),
                    likes: 0,
                    shares: 0,
                    likedBy: new Set()
                };
                
                this.posts.unshift(post);
                this.comments.set(post.id, []);
                
                if (this.users.has(userId)) {
                    this.users.get(userId).postsCount++;
                }
                
                this.extractHashtags(content);
                
                return post;
            }

            addComment(postId, userId, content, timestamp = Date.now()) {
                const comment = {
                    id: this.nextCommentId++,
                    postId,
                    userId,
                    content,
                    timestamp
                };
                
                if (!this.comments.has(postId)) {
                    this.comments.set(postId, []);
                }
                
                this.comments.get(postId).push(comment);
                
                // 如果不是自己評論自己的貼文，發送通知
                const post = this.posts.find(p => p.id === postId);
                if (post && post.userId !== userId) {
                    this.addNotification('comment', userId, `評論了你的發文：「${content.substring(0, 20)}${content.length > 20 ? '...' : ''}」`, timestamp, post.userId);
                }
                
                return comment;
            }

            getPostComments(postId) {
                return this.comments.get(postId) || [];
            }

            toggleLike(postId, userId) {
                const post = this.posts.find(p => p.id === postId);
                if (post) {
                    if (post.likedBy.has(userId)) {
                        post.likedBy.delete(userId);
                        post.likes--;
                    } else {
                        post.likedBy.add(userId);
                        post.likes++;
                        
                        if (post.userId !== userId) {
                            this.addNotification('like', userId, '喜歡了你的發文', Date.now(), post.userId);
                        }
                    }
                    return post.likedBy.has(userId);
                }
                return false;
            }

            followUser(followerId, followedId) {
                if (followerId === followedId) return false;
                
                const follower = this.users.get(followerId);
                const followed = this.users.get(followedId);
                
                if (follower && followed) {
                    if (!follower.following.has(followedId)) {
                        follower.following.add(followedId);
                        followed.followers.add(followerId);
                        
                        this.addNotification('follow', followerId, '開始關注你', Date.now(), followedId);
                        return true;
                    }
                }
                return false;
            }

            unfollowUser(followerId, followedId) {
                const follower = this.users.get(followerId);
                const followed = this.users.get(followedId);
                
                if (follower && followed) {
                    follower.following.delete(followedId);
                    followed.followers.delete(followerId);
                    return true;
                }
                return false;
            }

            isFollowing(followerId, followedId) {
                const follower = this.users.get(followerId);
                return follower ? follower.following.has(followedId) : false;
            }

            addNotification(type, fromUserId, message, timestamp = Date.now(), toUserId = null) {
                const targetUserId = toUserId || (this.currentUser ? this.currentUser.id : null);
                if (!targetUserId) return null;
                
                const notification = {
                    id: this.nextNotificationId++,
                    type,
                    fromUserId,
                    toUserId: targetUserId,
                    message,
                    timestamp,
                    read: false
                };
                this.notifications.unshift(notification);
                return notification;
            }

            getFilteredPosts() {
                if (!this.isLoggedIn || this.feedFilter === 'all') {
                    return this.posts;
                }
                
                if (this.feedFilter === 'following') {
                    const followingIds = this.currentUser.following;
                    return this.posts.filter(post => 
                        followingIds.has(post.userId) || post.userId === this.currentUser.id
                    );
                }
                
                return this.posts;
            }

            extractHashtags(content) {
                const hashtags = content.match(/#[\u4e00-\u9fa5a-zA-Z0-9_]+/g);
                if (hashtags) {
                    hashtags.forEach(tag => {
                        const cleanTag = tag.substring(1);
                        this.hashtags.set(cleanTag, (this.hashtags.get(cleanTag) || 0) + 1);
                    });
                }
            }

            updateTrendingTags() {
                const sortedTags = Array.from(this.hashtags.entries())
                    .sort((a, b) => b[1] - a[1])
                    .slice(0, 8);
                
                const container = document.getElementById('trending-tags');
                container.innerHTML = sortedTags.map(([tag, count]) => 
                    `<a href="#" class="block text-primary hover:underline">#${tag} <span class="text-gray-500 text-xs">(${count})</span></a>`
                ).join('');
            }

            getFormattedTime(timestamp) {
                const now = Date.now();
                const diff = now - timestamp;
                
                const minutes = Math.floor(diff / (1000 * 60));
                const hours = Math.floor(diff / (1000 * 60 * 60));
                const days = Math.floor(diff / (1000 * 60 * 60 * 24));
                
                if (minutes < 1) return '剛剛';
                if (minutes < 60) return `${minutes}分鐘前`;
                if (hours < 24) return `${hours}小時前`;
                return `${days}天前`;
            }

            updateProfile(username, bio) {
                if (this.currentUser) {
                    this.currentUser.username = username;
                    this.currentUser.bio = bio;
                    return true;
                }
                return false;
            }
        }

        // 初始化應用程式
        const app = new AppState();

        // Dark mode detection
        if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            document.documentElement.classList.add('dark');
        }
        window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
            if (event.matches) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        });

        // DOM 元素
        const elements = {
            authModal: document.getElementById('auth-modal'),
            authBtn: document.getElementById('auth-btn'),
            closeModal: document.getElementById('close-modal'),
            toggleAuth: document.getElementById('toggle-auth'),
            authForm: document.getElementById('auth-form'),
            authTitle: document.getElementById('auth-title'),
            authSubmitText: document.getElementById('auth-submit-text'),
            toggleAuthText: document.getElementById('toggle-auth-text'),
            registerFields: document.getElementById('register-fields'),
            userMenu: document.getElementById('user-menu'),
            userMenuBtn: document.getElementById('user-menu-btn'),
            userDropdown: document.getElementById('user-dropdown'),
            logoutBtn: document.getElementById('logout-btn'),
            createPostSection: document.getElementById('create-post-section'),
            postBtn: document.getElementById('post-btn'),
            postContent: document.getElementById('post-content'),
            postsContainer: document.getElementById('posts-container'),
            imageBtn: document.getElementById('image-btn'),
            imageUpload: document.getElementById('image-upload'),
            profileEditModal: document.getElementById('profile-edit-modal'),
            editProfileBtn: document.getElementById('edit-profile-btn'),
            closeProfileModal: document.getElementById('close-profile-modal'),
            profileEditForm: document.getElementById('profile-edit-form'),
            notificationBadge: document.getElementById('notification-badge'),
            userProfileModal: document.getElementById('user-profile-modal'),
            closeUserProfileModal: document.getElementById('close-user-profile-modal'),
            commentModal: document.getElementById('comment-modal'),
            closeCommentModal: document.getElementById('close-comment-modal'),
            discoverContainer: document.getElementById('discover-container'),
            feedFilter: document.getElementById('feed-filter'),
            feedAll: document.getElementById('feed-all'),
            feedFollowing: document.getElementById('feed-following')
        };

        // 登入/註冊功能
        let isLogin = true;

        elements.authBtn.addEventListener('click', () => {
            elements.authModal.classList.remove('hidden');
        });

        elements.closeModal.addEventListener('click', () => {
            elements.authModal.classList.add('hidden');
        });

        elements.toggleAuth.addEventListener('click', () => {
            isLogin = !isLogin;
            if (isLogin) {
                elements.authTitle.textContent = '登入';
                elements.authSubmitText.textContent = '登入';
                elements.toggleAuthText.textContent = '還沒有帳戶？註冊';
                elements.registerFields.classList.add('hidden');
            } else {
                elements.authTitle.textContent = '註冊';
                elements.authSubmitText.textContent = '註冊';
                elements.toggleAuthText.textContent = '已有帳戶？登入';
                elements.registerFields.classList.remove('hidden');
            }
        });

        elements.authForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const email = document.getElementById('email').value.trim();
            const password = document.getElementById('password').value.trim();
            
            if (!email || !password) {
                showNotification('請填寫所有必填欄位', 'error');
                return;
            }

            let result;
            if (isLogin) {
                result = app.login(email, password);
            } else {
                const username = document.getElementById('username').value.trim();
                if (!username) {
                    showNotification('請輸入用戶名', 'error');
                    return;
                }
                result = app.register(username, email, password);
            }

            if (result.success) {
                elements.authModal.classList.add('hidden');
                updateUIAfterLogin();
                showNotification(isLogin ? '登入成功！' : '註冊成功！', 'success');
                elements.authForm.reset();
            } else {
                showNotification(result.message, 'error');
            }
        });

        // 登出功能
        elements.userMenuBtn.addEventListener('click', () => {
            elements.userDropdown.classList.toggle('hidden');
        });

        elements.logoutBtn.addEventListener('click', () => {
            app.logout();
            updateUIAfterLogout();
            elements.userDropdown.classList.add('hidden');
            showNotification('已登出', 'info');
        });

        // 動態篩選功能
        elements.feedAll.addEventListener('click', () => {
            app.feedFilter = 'all';
            elements.feedAll.className = 'px-4 py-2 rounded-lg bg-primary text-white';
            elements.feedFollowing.className = 'px-4 py-2 rounded-lg bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300';
            renderPosts();
        });

        elements.feedFollowing.addEventListener('click', () => {
            if (!app.isLoggedIn) {
                showNotification('請先登入', 'error');
                return;
            }
            app.feedFilter = 'following';
            elements.feedFollowing.className = 'px-4 py-2 rounded-lg bg-primary text-white';
            elements.feedAll.className = 'px-4 py-2 rounded-lg bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300';
            renderPosts();
        });

        // 點擊其他地方關閉下拉選單
        document.addEventListener('click', (e) => {
            if (!elements.userMenuBtn.contains(e.target)) {
                elements.userDropdown.classList.add('hidden');
            }
        });

        // 發文功能
        elements.postBtn.addEventListener('click', () => {
            const content = elements.postContent.value.trim();
            if (content && app.isLoggedIn) {
                const post = app.createPost(app.currentUser.id, content);
                elements.postContent.value = '';
                renderPosts();
                updateUserStats();
                app.updateTrendingTags();
                showNotification('發文成功！', 'success');
            } else if (!app.isLoggedIn) {
                showNotification('請先登入', 'error');
            } else {
                showNotification('請輸入內容', 'error');
            }
        });

        // 圖片上傳功能
        elements.imageBtn.addEventListener('click', () => {
            elements.imageUpload.click();
        });

        elements.imageUpload.addEventListener('change', (e) => {
            const file = e.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = (e) => {
                    showNotification('圖片已選擇（演示功能）', 'info');
                };
                reader.readAsDataURL(file);
            }
        });

        // 個人資料編輯功能
        elements.editProfileBtn.addEventListener('click', () => {
            if (app.currentUser) {
                document.getElementById('profile-username').value = app.currentUser.username;
                document.getElementById('profile-bio').value = app.currentUser.bio;
                elements.profileEditModal.classList.remove('hidden');
            }
        });

        elements.closeProfileModal.addEventListener('click', () => {
            elements.profileEditModal.classList.add('hidden');
        });

        elements.profileEditForm.addEventListener('submit', (e) => {
            e.preventDefault();
            const username = document.getElementById('profile-username').value.trim();
            const bio = document.getElementById('profile-bio').value.trim();
            
            if (username) {
                app.updateProfile(username, bio);
                updateUserProfile();
                elements.profileEditModal.classList.add('hidden');
                showNotification('個人資料已更新', 'success');
            } else {
                showNotification('用戶名不能為空', 'error');
            }
        });

        // 關閉模態框
        elements.closeUserProfileModal.addEventListener('click', () => {
            elements.userProfileModal.classList.add('hidden');
        });

        elements.closeCommentModal.addEventListener('click', () => {
            elements.commentModal.classList.add('hidden');
        });

        // UI 更新函數
        function updateUIAfterLogin() {
            elements.authBtn.classList.add('hidden');
            elements.userMenu.classList.remove('hidden');
            elements.createPostSection.classList.remove('hidden');
            elements.editProfileBtn.classList.remove('hidden');
            elements.feedFilter.classList.remove('hidden');
            
            updateUserProfile();
            updateUserStats();
            renderPosts();
            renderNotifications();
            renderDiscoverUsers();
        }

        function updateUIAfterLogout() {
            elements.authBtn.classList.remove('hidden');
            elements.userMenu.classList.add('hidden');
            elements.createPostSection.classList.add('hidden');
            elements.editProfileBtn.classList.add('hidden');
            elements.feedFilter.classList.add('hidden');
            
            // 重置篩選
            app.feedFilter = 'all';
            elements.feedAll.className = 'px-4 py-2 rounded-lg bg-primary text-white';
            elements.feedFollowing.className = 'px-4 py-2 rounded-lg bg-gray-200 dark:bg-gray-700 text-gray-700 dark:text-gray-300';
            
            // 重置用戶界面
            document.getElementById('sidebar-username').textContent = '請先登入';
            document.getElementById('sidebar-handle').textContent = '@guest';
            document.getElementById('sidebar-posts').textContent = '0';
            document.getElementById('sidebar-following').textContent = '0';
            document.getElementById('sidebar-followers').textContent = '0';
            
            document.getElementById('profile-name').textContent = '請先登入';
            document.getElementById('profile-handle').textContent = '@guest';
            document.getElementById('profile-bio').textContent = '請登入後編輯您的個人簡介';
            
            renderPosts();
            renderDiscoverUsers();
        }

        function updateUserProfile() {
            if (app.currentUser) {
                const user = app.currentUser;
                
                document.getElementById('user-name').textContent = user.username;
                document.getElementById('user-avatar').src = user.avatar;
                document.getElementById('sidebar-avatar').src = user.avatar;
                document.getElementById('sidebar-username').textContent = user.username;
                document.getElementById('sidebar-handle').textContent = `@${user.username.toLowerCase()}`;
                document.getElementById('create-post-avatar').src = user.avatar;
                
                document.getElementById('profile-avatar').src = user.avatar;
                document.getElementById('profile-name').textContent = user.username;
                document.getElementById('profile-handle').textContent = `@${user.username.toLowerCase()}`;
                document.getElementById('profile-bio').textContent = user.bio || '這位用戶還沒有設置個人簡介';
            }
        }

        function updateUserStats() {
            if (app.currentUser) {
                const user = app.currentUser;
                
                document.getElementById('sidebar-posts').textContent = user.postsCount;
                document.getElementById('sidebar-following').textContent = user.following.size;
                document.getElementById('sidebar-followers').textContent = user.followers.size;
                
                document.getElementById('profile-posts-count').textContent = user.postsCount;
                document.getElementById('profile-following-count').textContent = user.following.size;
                document.getElementById('profile-followers-count').textContent = user.followers.size;
            }
        }

        function renderPosts() {
            elements.postsContainer.innerHTML = '';
            
            const posts = app.getFilteredPosts();
            
            if (posts.length === 0) {
                elements.postsContainer.innerHTML = '<div class="text-center text-gray-500 py-8">目前沒有貼文</div>';
                return;
            }
            
            posts.forEach(post => {
                const user = app.users.get(post.userId);
                if (user) {
                    const postElement = createPostElement(post, user);
                    elements.postsContainer.appendChild(postElement);
                }
            });
        }

        function createPostElement(post, user) {
            const postDiv = document.createElement('div');
            postDiv.className = 'bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6';
            
            const isLiked = app.currentUser && post.likedBy.has(app.currentUser.id);
            const likeClass = isLiked ? 'fas fa-heart text-red-500' : 'far fa-heart';
            
            const comments = app.getPostComments(post.id);
            const commentCount = comments.length;
            
            postDiv.innerHTML = `
                <div class="flex items-center space-x-3 mb-4">
                    <img class="w-10 h-10 rounded-full cursor-pointer hover:opacity-80" src="${user.avatar}" alt="${user.username}" onclick="showUserProfile(${user.id})">
                    <div>
                        <p class="font-semibold cursor-pointer hover:underline" onclick="showUserProfile(${user.id})">${user.username}</p>
                        <p class="text-sm text-gray-500">${app.getFormattedTime(post.timestamp)}</p>
                    </div>
                </div>
                <p class="mb-4">${formatPostContent(post.content)}</p>
                ${post.image ? `<img class="w-full h-64 object-cover rounded-lg mb-4" src="${post.image}" alt="Post image">` : ''}
                <div class="flex items-center space-x-6 text-gray-500">
                    <button class="flex items-center space-x-1 hover:text-red-500 transition-colors like-btn" data-post-id="${post.id}">
                        <i class="${likeClass}"></i>
                        <span>${post.likes}</span>
                    </button>
                    <button class="flex items-center space-x-1 hover:text-blue-500 transition-colors comment-btn" data-post-id="${post.id}">
                        <i class="far fa-comment"></i>
                        <span>${commentCount}</span>
                    </button>
                    <button class="flex items-center space-x-1 hover:text-green-500 transition-colors">
                        <i class="fas fa-share"></i>
                        <span>${post.shares}</span>
                    </button>
                </div>
            `;
            
            // 添加點讚功能
            const likeBtn = postDiv.querySelector('.like-btn');
            likeBtn.addEventListener('click', () => {
                if (app.isLoggedIn) {
                    const liked = app.toggleLike(post.id, app.currentUser.id);
                    const heartIcon = likeBtn.querySelector('i');
                    const likeCount = likeBtn.querySelector('span');
                    
                    if (liked) {
                        heartIcon.className = 'fas fa-heart text-red-500';
                    } else {
                        heartIcon.className = 'far fa-heart';
                    }
                    likeCount.textContent = post.likes;
                    
                    if (app.currentUser.id !== post.userId) {
                        renderNotifications();
                    }
                } else {
                    showNotification('請先登入', 'error');
                }
            });
            
            // 添加評論功能
            const commentBtn = postDiv.querySelector('.comment-btn');
            commentBtn.addEventListener('click', () => {
                showCommentModal(post.id);
            });
            
            return postDiv;
        }

        function showUserProfile(userId) {
            const user = app.users.get(userId);
            if (!user) return;
            
            const isOwnProfile = app.currentUser && app.currentUser.id === userId;
            const isFollowing = app.currentUser && app.isFollowing(app.currentUser.id, userId);
            
            const userPosts = app.posts.filter(post => post.userId === userId);
            
            document.getElementById('user-profile-content').innerHTML = `
                <div class="flex flex-col md:flex-row items-center md:items-start space-y-4 md:space-y-0 md:space-x-8 mb-8">
                    <img class="w-32 h-32 rounded-full" src="${user.avatar}" alt="${user.username}">
                    <div class="flex-1 text-center md:text-left">
                        <h2 class="text-3xl font-bold mb-2">${user.username}</h2>
                        <p class="text-gray-500 mb-4">@${user.username.toLowerCase()}</p>
                        <p class="mb-6">${user.bio || '這位用戶還沒有設置個人簡介'}</p>
                        <div class="flex justify-center md:justify-start space-x-6 mb-6">
                            <div class="text-center">
                                <p class="font-bold text-xl">${user.postsCount}</p>
                                <p class="text-gray-500">發文</p>
                            </div>
                            <div class="text-center">
                                <p class="font-bold text-xl">${user.following.size}</p>
                                <p class="text-gray-500">關注</p>
                            </div>
                            <div class="text-center">
                                <p class="font-bold text-xl">${user.followers.size}</p>
                                <p class="text-gray-500">粉絲</p>
                            </div>
                        </div>
                        ${!isOwnProfile && app.isLoggedIn ? `
                            <button onclick="toggleFollow(${userId})" class="px-6 py-2 rounded-lg transition-colors ${isFollowing ? 'bg-gray-500 text-white' : 'bg-primary text-white hover:bg-primary-dark'}">
                                ${isFollowing ? '取消關注' : '關注'}
                            </button>
                        ` : ''}
                    </div>
                </div>
                <div>
                    <h3 class="text-xl font-bold mb-4">用戶發文</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        ${userPosts.length === 0 ? '<p class="text-gray-500 col-span-2 text-center">這位用戶還沒有發布任何貼文</p>' : userPosts.map(post => `
                            <div class="bg-gray-100 dark:bg-gray-700 rounded-lg p-4">
                                <p class="mb-2">${formatPostContent(post.content.substring(0, 100))}${post.content.length > 100 ? '...' : ''}</p>
                                ${post.image ? `<img class="w-full h-32 object-cover rounded mb-2" src="${post.image}" alt="Post image">` : ''}
                                <p class="text-sm text-gray-500">${app.getFormattedTime(post.timestamp)}</p>
                            </div>
                        `).join('')}
                    </div>
                </div>
            `;
            
            elements.userProfileModal.classList.remove('hidden');
        }

        function showCommentModal(postId) {
            const post = app.posts.find(p => p.id === postId);
            const postUser = app.users.get(post.userId);
            const comments = app.getPostComments(postId);
            
            document.getElementById('comment-content').innerHTML = `
                <div class="mb-6 pb-6 border-b border-gray-200 dark:border-gray-700">
                    <div class="flex items-center space-x-3 mb-4">
                        <img class="w-10 h-10 rounded-full" src="${postUser.avatar}" alt="${postUser.username}">
                        <div>
                            <p class="font-semibold">${postUser.username}</p>
                            <p class="text-sm text-gray-500">${app.getFormattedTime(post.timestamp)}</p>
                        </div>
                    </div>
                    <p>${formatPostContent(post.content)}</p>
                    ${post.image ? `<img class="w-full h-64 object-cover rounded-lg mt-4" src="${post.image}" alt="Post image">` : ''}
                </div>
                
                ${app.isLoggedIn ? `
                    <div class="mb-6">
                        <div class="flex space-x-3">
                            <img class="w-8 h-8 rounded-full" src="${app.currentUser.avatar}" alt="${app.currentUser.username}">
                            <div class="flex-1">
                                <textarea id="comment-input" placeholder="寫下你的評論..." class="w-full p-3 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary resize-none text-base bg-white dark:bg-gray-700" rows="2"></textarea>
                                <button onclick="addComment(${postId})" class="mt-2 bg-primary hover:bg-primary-dark text-white px-4 py-2 rounded-lg transition-colors">
                                    發布評論
                                </button>
                            </div>
                        </div>
                    </div>
                ` : ''}
                
                <div id="comments-list" class="space-y-4">
                    ${comments.length === 0 ? '<p class="text-gray-500 text-center">目前沒有評論</p>' : comments.map(comment => {
                        const commentUser = app.users.get(comment.userId);
                        return `
                            <div class="flex space-x-3">
                                <img class="w-8 h-8 rounded-full" src="${commentUser.avatar}" alt="${commentUser.username}">
                                <div class="flex-1">
                                    <div class="bg-gray-100 dark:bg-gray-700 rounded-lg p-3">
                                        <p class="font-semibold text-sm">${commentUser.username}</p>
                                        <p>${comment.content}</p>
                                    </div>
                                    <p class="text-xs text-gray-500 mt-1">${app.getFormattedTime(comment.timestamp)}</p>
                                </div>
                            </div>
                        `;
                    }).join('')}
                </div>
            `;
            
            elements.commentModal.classList.remove('hidden');
        }

        function addComment(postId) {
            const commentInput = document.getElementById('comment-input');
            const content = commentInput.value.trim();
            
            if (content && app.isLoggedIn) {
                app.addComment(postId, app.currentUser.id, content);
                commentInput.value = '';
                showCommentModal(postId); // 重新渲染評論
                renderPosts(); // 更新主頁的評論數
                renderNotifications(); // 更新通知
                showNotification('評論已發布！', 'success');
            } else if (!app.isLoggedIn) {
                showNotification('請先登入', 'error');
            } else {
                showNotification('請輸入評論內容', 'error');
            }
        }

        function toggleFollow(userId) {
            if (!app.isLoggedIn) {
                showNotification('請先登入', 'error');
                return;
            }
            
            const isFollowing = app.isFollowing(app.currentUser.id, userId);
            
            if (isFollowing) {
                app.unfollowUser(app.currentUser.id, userId);
                showNotification('已取消關注', 'info');
            } else {
                app.followUser(app.currentUser.id, userId);
                showNotification('關注成功', 'success');
                renderNotifications();
            }
            
            updateUserStats();
            showUserProfile(userId); // 重新渲染用戶資料
            renderDiscoverUsers(); // 更新探索頁面
        }

        function renderDiscoverUsers() {
            elements.discoverContainer.innerHTML = '';
            
            Array.from(app.users.values()).forEach(user => {
                if (app.currentUser && user.id === app.currentUser.id) return;
                
                const isFollowing = app.currentUser && app.isFollowing(app.currentUser.id, user.id);
                
                const userCard = document.createElement('div');
                userCard.className = 'bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 text-center';
                
                userCard.innerHTML = `
                    <img class="w-20 h-20 rounded-full mx-auto mb-4 cursor-pointer hover:opacity-80" src="${user.avatar}" alt="${user.username}" onclick="showUserProfile(${user.id})">
                    <h3 class="font-bold text-lg mb-2 cursor-pointer hover:underline" onclick="showUserProfile(${user.id})">${user.username}</h3>
                    <p class="text-gray-500 mb-4">@${user.username.toLowerCase()}</p>
                    <p class="text-sm mb-4">${user.bio || '這位用戶還沒有設置個人簡介'}</p>
                    <div class="flex justify-center space-x-4 mb-4 text-sm">
                        <div>
                            <span class="font-bold">${user.postsCount}</span>
                            <span class="text-gray-500">發文</span>
                        </div>
                        <div>
                            <span class="font-bold">${user.followers.size}</span>
                            <span class="text-gray-500">粉絲</span>
                        </div>
                    </div>
                    ${app.isLoggedIn ? `
                        <button onclick="toggleFollow(${user.id})" class="w-full px-4 py-2 rounded-lg transition-colors ${isFollowing ? 'bg-gray-500 text-white' : 'bg-primary text-white hover:bg-primary-dark'}">
                            ${isFollowing ? '取消關注' : '關注'}
                        </button>
                    ` : ''}
                `;
                
                elements.discoverContainer.appendChild(userCard);
            });
            
            if (elements.discoverContainer.children.length === 0) {
                elements.discoverContainer.innerHTML = '<div class="col-span-3 text-center text-gray-500">沒有其他用戶</div>';
            }
        }

        function formatPostContent(content) {
            return content.replace(/#([\u4e00-\u9fa5a-zA-Z0-9_]+)/g, 
                '<span class="text-primary font-medium">#$1</span>');
        }

        function renderNotifications() {
            const container = document.getElementById('notifications-container');
            container.innerHTML = '';
            
            const userNotifications = app.notifications.filter(n => 
                !app.currentUser || n.toUserId === app.currentUser.id
            );
            
            if (userNotifications.length === 0) {
                container.innerHTML = '<p class="p-6 text-gray-500 text-center">目前沒有通知</p>';
                elements.notificationBadge.textContent = '0';
                return;
            }
            
            userNotifications.forEach(notification => {
                const fromUser = app.users.get(notification.fromUserId);
                if (fromUser) {
                    const notifElement = document.createElement('div');
                    notifElement.className = `p-6 hover:bg-gray-50 dark:hover:bg-gray-700 transition-colors ${!notification.read ? 'bg-blue-50 dark:bg-blue-900' : ''}`;
                    
                    notifElement.innerHTML = `
                        <div class="flex items-center space-x-4">
                            <img class="w-10 h-10 rounded-full cursor-pointer hover:opacity-80" src="${fromUser.avatar}" alt="${fromUser.username}" onclick="showUserProfile(${fromUser.id})">
                            <div class="flex-1">
                                <p><span class="font-semibold cursor-pointer hover:underline" onclick="showUserProfile(${fromUser.id})">${fromUser.username}</span> ${notification.message}</p>
                                <p class="text-sm text-gray-500">${app.getFormattedTime(notification.timestamp)}</p>
                            </div>
                            ${!notification.read ? '<div class="w-3 h-3 bg-primary rounded-full"></div>' : ''}
                        </div>
                    `;
                    
                    container.appendChild(notifElement);
                }
            });
            
            const unreadCount = userNotifications.filter(n => !n.read).length;
            elements.notificationBadge.textContent = unreadCount;
            elements.notificationBadge.classList.toggle('hidden', unreadCount === 0);
        }

        // 導航功能
        const navLinks = document.querySelectorAll('.nav-link, .nav-link-mobile');
        const tabContents = document.querySelectorAll('.tab-content');

        navLinks.forEach(link => {
            link.addEventListener('click', (e) => {
                e.preventDefault();
                const targetTab = link.getAttribute('data-tab');
                
                navLinks.forEach(nl => nl.classList.remove('active'));
                link.classList.add('active');
                
                tabContents.forEach(tab => tab.classList.add('hidden'));
                
                document.getElementById(`${targetTab}-tab`).classList.remove('hidden');
                
                if (targetTab === 'notifications' && app.currentUser) {
                    app.notifications.forEach(n => {
                        if (n.toUserId === app.currentUser.id) n.read = true;
                    });
                    renderNotifications();
                } else if (targetTab === 'discover') {
                    renderDiscoverUsers();
                }
            });
        });

        // 通知系統
        function showNotification(message, type = 'info') {
            const notification = document.createElement('div');
            notification.className = `fixed top-4 right-4 p-4 rounded-lg shadow-lg z-50 transition-all transform translate-x-full max-w-sm`;
            
            if (type === 'success') {
                notification.className += ' bg-green-500 text-white';
            } else if (type === 'error') {
                notification.className += ' bg-red-500 text-white';
            } else {
                notification.className += ' bg-blue-500 text-white';
            }
            
            notification.innerHTML = `
                <div class="flex items-center space-x-2">
                    <span>${message}</span>
                    <button onclick="this.parentElement.parentElement.remove()" class="ml-2 hover:bg-black hover:bg-opacity-20 rounded px-2 py-1">
                        <i class="fas fa-times"></i>
                    </button>
                </div>
            `;
            
            document.body.appendChild(notification);
            
            setTimeout(() => {
                notification.classList.remove('translate-x-full');
            }, 100);
            
            setTimeout(() => {
                notification.classList.add('translate-x-full');
                setTimeout(() => {
                    if (notification.parentNode) {
                        notification.remove();
                    }
                }, 300);
            }, 4000);
        }

        // 初始化 CSS 樣式
        const style = document.createElement('style');
        style.textContent = `
            .nav-link {
                @apply px-3 py-2 rounded-md text-sm font-medium text-gray-500 hover:text-gray-700 dark:text-gray-300 dark:hover:text-white transition-colors;
            }
            .nav-link.active {
                @apply text-primary bg-gray-100 dark:bg-gray-700;
            }
            .nav-link-mobile {
                @apply p-3 text-gray-500 hover:text-primary dark:text-gray-300 dark:hover:text-primary transition-colors;
            }
            .nav-link-mobile.active {
                @apply text-primary;
            }
        `;
        document.head.appendChild(style);

        // 初始化應用程式
        renderPosts();
        renderNotifications();
        renderDiscoverUsers();
    </script>
</body>
</html>
<!-- ...前面內容省略... -->
    <script>
        // 應用程式狀態管理
        class AppState {
            // ...（已完整提供，略）...
        }

        // 初始化應用程式
        const app = new AppState();

        // Dark mode detection
        if (window.matchMedia && window.matchMedia('(prefers-color-scheme: dark)').matches) {
            document.documentElement.classList.add('dark');
        }
        window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', event => {
            if (event.matches) {
                document.documentElement.classList.add('dark');
            } else {
                document.documentElement.classList.remove('dark');
            }
        });

        // DOM 元素
        const elements = {
            authModal: document.getElementById('auth-modal'),
            authBtn: document.getElementById('auth-btn'),
            closeModal: document.getElementById('close-modal'),
            toggleAuth: document.getElementById('toggle-auth'),
            authForm: document.getElementById('auth-form'),
            authTitle: document.getElementById('auth-title'),
            authSubmitText: document.getElementById('auth-submit-text'),
            toggleAuthText: document.getElementById('toggle-auth-text'),
            registerFields: document.getElementById('register-fields'),
            userMenu: document.getElementById('user-menu'),
            userMenuBtn: document.getElementById('user-menu-btn'),
            userDropdown: document.getElementById('user-dropdown'),
            logoutBtn: document.getElementById('logout-btn'),
            userAvatar: document.getElementById('user-avatar'),
            userName: document.getElementById('user-name'),
            notificationBadge: document.getElementById('notification-badge'),
            sidebarAvatar: document.getElementById('sidebar-avatar'),
            sidebarUsername: document.getElementById('sidebar-username'),
            sidebarHandle: document.getElementById('sidebar-handle'),
            sidebarPosts: document.getElementById('sidebar-posts'),
            sidebarFollowing: document.getElementById('sidebar-following'),
            sidebarFollowers: document.getElementById('sidebar-followers'),
            trendingTags: document.getElementById('trending-tags'),
            createPostSection: document.getElementById('create-post-section'),
            createPostAvatar: document.getElementById('create-post-avatar'),
            postContent: document.getElementById('post-content'),
            imageBtn: document.getElementById('image-btn'),
            imageUpload: document.getElementById('image-upload'),
            hashtagBtn: document.getElementById('hashtag-btn'),
            postBtn: document.getElementById('post-btn'),
            feedFilter: document.getElementById('feed-filter'),
            feedAll: document.getElementById('feed-all'),
            feedFollowing: document.getElementById('feed-following'),
            postsContainer: document.getElementById('posts-container'),
            profileEditModal: document.getElementById('profile-edit-modal'),
            closeProfileModal: document.getElementById('close-profile-modal'),
            profileEditForm: document.getElementById('profile-edit-form'),
            profileUsername: document.getElementById('profile-username'),
            profileBio: document.getElementById('profile-bio'),
            profileTab: document.getElementById('profile-tab'),
            profileAvatar: document.getElementById('profile-avatar'),
            profileName: document.getElementById('profile-name'),
            profileHandle: document.getElementById('profile-handle'),
            profileBioText: document.getElementById('profile-bio-text'),
            profilePostsCount: document.getElementById('profile-posts-count'),
            profileFollowingCount: document.getElementById('profile-following-count'),
            profileFollowersCount: document.getElementById('profile-followers-count'),
            editProfileBtn: document.getElementById('edit-profile-btn'),
            userPostsContainer: document.getElementById('user-posts-container'),
            userProfileModal: document.getElementById('user-profile-modal'),
            closeUserProfileModal: document.getElementById('close-user-profile-modal'),
            userProfileContent: document.getElementById('user-profile-content'),
            commentModal: document.getElementById('comment-modal'),
            closeCommentModal: document.getElementById('close-comment-modal'),
            commentContent: document.getElementById('comment-content'),
            discoverTab: document.getElementById('discover-tab'),
            discoverContainer: document.getElementById('discover-container'),
            aboutTab: document.getElementById('about-tab'),
            notificationsTab: document.getElementById('notifications-tab'),
            notificationsContainer: document.getElementById('notifications-container'),
            navLinks: document.querySelectorAll('.nav-link'),
            navLinksMobile: document.querySelectorAll('.nav-link-mobile'),
            homeTab: document.getElementById('home-tab'),
        };

        // Tab切換
        function showTab(tab) {
            document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
            let tabId = tab + '-tab';
            let tabEl = document.getElementById(tabId);
            if (tabEl) tabEl.classList.remove('hidden');

            elements.navLinks.forEach(link => {
                link.classList.toggle('active', link.dataset.tab === tab);
            });
            elements.navLinksMobile.forEach(link => {
                link.classList.toggle('active', link.dataset.tab === tab);
            });
        }

        elements.navLinks.forEach(link => {
            link.addEventListener('click', e => {
                e.preventDefault();
                showTab(link.dataset.tab);
                if (link.dataset.tab === 'profile') renderProfile();
                if (link.dataset.tab === 'notifications') renderNotifications();
                if (link.dataset.tab === 'discover') renderDiscover();
            });
        });
        elements.navLinksMobile.forEach(link => {
            link.addEventListener('click', e => {
                e.preventDefault();
                showTab(link.dataset.tab);
                if (link.dataset.tab === 'profile') renderProfile();
                if (link.dataset.tab === 'notifications') renderNotifications();
                if (link.dataset.tab === 'discover') renderDiscover();
            });
        });

        // 登入/註冊 Modal 控制
        elements.authBtn.addEventListener('click', () => {
            openAuthModal('login');
        });
        elements.closeModal.addEventListener('click', () => closeAuthModal());
        elements.toggleAuth.addEventListener('click', () => {
            if (elements.registerFields.classList.contains('hidden')) {
                openAuthModal('register');
            } else {
                openAuthModal('login');
            }
        });

        function openAuthModal(mode) {
            elements.authModal.classList.remove('hidden');
            if (mode === 'login') {
                elements.authTitle.textContent = '登入';
                elements.authSubmitText.textContent = '登入';
                elements.toggleAuthText.textContent = '還沒有帳戶？註冊';
                elements.registerFields.classList.add('hidden');
            } else {
                elements.authTitle.textContent = '註冊';
                elements.authSubmitText.textContent = '註冊';
                elements.toggleAuthText.textContent = '已有帳戶？登入';
                elements.registerFields.classList.remove('hidden');
            }
        }
        function closeAuthModal() {
            elements.authModal.classList.add('hidden');
            elements.authForm.reset();
        }

        // 登入/註冊 submit
        elements.authForm.addEventListener('submit', e => {
            e.preventDefault();
            const mode = elements.registerFields.classList.contains('hidden') ? 'login' : 'register';
            const email = document.getElementById('email').value;
            const password = document.getElementById('password').value;
            if (mode === 'login') {
                const result = app.login(email, password);
                if (result.success) {
                    closeAuthModal();
                    updateUIForLogin();
                } else {
                    alert(result.message);
                }
            } else {
                const username = document.getElementById('username').value;
                if (!username) {
                    alert('請輸入用戶名');
                    return;
                }
                const result = app.register(username, email, password);
                if (result.success) {
                    closeAuthModal();
                    updateUIForLogin();
                } else {
                    alert(result.message);
                }
            }
        });

        // 登出
        elements.logoutBtn.addEventListener('click', () => {
            app.logout();
            updateUIForLogout();
        });

        // 用戶下拉菜單
        elements.userMenuBtn.addEventListener('click', () => {
            elements.userDropdown.classList.toggle('hidden');
        });
        document.addEventListener('click', e => {
            if (!elements.userMenu.contains(e.target)) {
                elements.userDropdown.classList.add('hidden');
            }
        });

        // 更新登入/登出後的UI
        function updateUIForLogin() {
            elements.authBtn.classList.add('hidden');
            elements.userMenu.classList.remove('hidden');
            elements.userAvatar.src = app.currentUser.avatar;
            elements.userName.textContent = app.currentUser.username;
            elements.createPostSection.classList.remove('hidden');
            elements.feedFilter.classList.remove('hidden');
            renderSidebar();
            renderPosts();
            renderProfile();
        }
        function updateUIForLogout() {
            elements.authBtn.classList.remove('hidden');
            elements.userMenu.classList.add('hidden');
            elements.createPostSection.classList.add('hidden');
            elements.feedFilter.classList.add('hidden');
            renderSidebar();
            renderPosts();
            renderProfile();
        }

        // Sidebar個人資訊
        function renderSidebar() {
            if (app.isLoggedIn) {
                elements.sidebarAvatar.src = app.currentUser.avatar;
                elements.sidebarUsername.textContent = app.currentUser.username;
                elements.sidebarHandle.textContent = '@' + app.currentUser.username;
                elements.sidebarPosts.textContent = app.currentUser.postsCount;
                elements.sidebarFollowing.textContent = app.currentUser.following.size;
                elements.sidebarFollowers.textContent = app.currentUser.followers.size;
            } else {
                elements.sidebarAvatar.src = "https://ui-avatars.com/api/?name=Guest&background=CCCCCC&color=fff";
                elements.sidebarUsername.textContent = "請先登入";
                elements.sidebarHandle.textContent = "@guest";
                elements.sidebarPosts.textContent = "0";
                elements.sidebarFollowing.textContent = "0";
                elements.sidebarFollowers.textContent = "0";
            }
            app.updateTrendingTags();
        }

        // 貼文動態
        function renderPosts() {
            const posts = app.getFilteredPosts();
            elements.postsContainer.innerHTML = posts.map(post => {
                const user = app.users.get(post.userId);
                return `
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6">
                    <div class="flex items-center mb-4">
                        <img class="w-10 h-10 rounded-full mr-3" src="${user.avatar}" alt="${user.username}">
                        <div>
                            <p class="font-bold">${user.username}</p>
                            <p class="text-xs text-gray-500">${app.getFormattedTime(post.timestamp)}</p>
                        </div>
                    </div>
                    <p class="mb-4">${post.content.replace(/#[\u4e00-\u9fa5a-zA-Z0-9_]+/g, tag => `<span class="text-primary">${tag}</span>`)}</p>
                    ${post.image ? `<img class="rounded-lg mb-4 max-h-60 w-auto mx-auto" src="${post.image}">` : ""}
                    <div class="flex space-x-4">
                        <button class="like-btn ${post.likedBy.has(app.currentUser?.id) ? 'text-primary' : 'text-gray-500'}" data-id="${post.id}">
                            <i class="fas fa-heart"></i> ${post.likes}
                        </button>
                        <button class="comment-btn text-gray-500" data-id="${post.id}">
                            <i class="fas fa-comment"></i> ${app.getPostComments(post.id).length}
                        </button>
                        <button class="share-btn text-gray-500" data-id="${post.id}">
                            <i class="fas fa-share"></i> ${post.shares}
                        </button>
                    </div>
                </div>`;
            }).join('');
        }

        // 按讚功能
        elements.postsContainer.addEventListener('click', function(e) {
            if (e.target.closest('.like-btn')) {
                const btn = e.target.closest('.like-btn');
                const postId = parseInt(btn.dataset.id);
                if (!app.isLoggedIn) {
                    openAuthModal('login');
                    return;
                }
                app.toggleLike(postId, app.currentUser.id);
                renderPosts();
                renderSidebar();
            }
            if (e.target.closest('.comment-btn')) {
                const btn = e.target.closest('.comment-btn');
                const postId = parseInt(btn.dataset.id);
                renderComments(postId);
            }
        });

        // 發布貼文
        elements.postBtn.addEventListener('click', () => {
            if (!app.isLoggedIn) {
                openAuthModal('login');
                return;
            }
            const content = elements.postContent.value;
            let image = elements.imageUpload.files[0];
            let imageUrl = null;
            if (image) {
                // 模擬圖片上傳
                imageUrl = URL.createObjectURL(image);
            }
            if (content.trim() === "") {
                alert("內容不可為空");
                return;
            }
            app.createPost(app.currentUser.id, content, imageUrl);
            elements.postContent.value = "";
            elements.imageUpload.value = "";
            renderPosts();
            renderSidebar();
        });

        // 上傳圖片按鈕
        elements.imageBtn.addEventListener('click', () => {
            elements.imageUpload.click();
        });

        // Feed過濾
        elements.feedAll.addEventListener('click', () => {
            app.feedFilter = 'all';
            elements.feedAll.classList.add('bg-primary', 'text-white');
            elements.feedFollowing.classList.remove('bg-primary', 'text-white');
            renderPosts();
        });
        elements.feedFollowing.addEventListener('click', () => {
            app.feedFilter = 'following';
            elements.feedFollowing.classList.add('bg-primary', 'text-white');
            elements.feedAll.classList.remove('bg-primary', 'text-white');
            renderPosts();
        });

        // 編輯個人資料
        elements.editProfileBtn.addEventListener('click', () => {
            elements.profileEditModal.classList.remove('hidden');
            elements.profileUsername.value = app.currentUser.username;
            elements.profileBio.value = app.currentUser.bio || "";
        });
        elements.closeProfileModal.addEventListener('click', () => {
            elements.profileEditModal.classList.add('hidden');
        });
        elements.profileEditForm.addEventListener('submit', e => {
            e.preventDefault();
            const username = elements.profileUsername.value;
            const bio = elements.profileBio.value;
            app.updateProfile(username, bio);
            elements.profileEditModal.classList.add('hidden');
            renderProfile();
            renderSidebar();
        });

        // Profile資料呈現
        function renderProfile() {
            if (!app.isLoggedIn) {
                elements.profileAvatar.src = "https://ui-avatars.com/api/?name=Guest&background=CCCCCC&color=fff";
                elements.profileName.textContent = "請先登入";
                elements.profileHandle.textContent = "@guest";
                elements.profileBioText.textContent = "請登入後編輯您的個人簡介";
                elements.profilePostsCount.textContent = "0";
                elements.profileFollowingCount.textContent = "0";
                elements.profileFollowersCount.textContent = "0";
                elements.editProfileBtn.classList.add('hidden');
                elements.userPostsContainer.innerHTML = "";
            } else {
                elements.profileAvatar.src = app.currentUser.avatar;
                elements.profileName.textContent = app.currentUser.username;
                elements.profileHandle.textContent = "@" + app.currentUser.username;
                elements.profileBioText.textContent = app.currentUser.bio || "";
                elements.profilePostsCount.textContent = app.currentUser.postsCount;
                elements.profileFollowingCount.textContent = app.currentUser.following.size;
                elements.profileFollowersCount.textContent = app.currentUser.followers.size;
                elements.editProfileBtn.classList.remove('hidden');
                // 我的貼文
                const myPosts = app.posts.filter(p => p.userId === app.currentUser.id);
                elements.userPostsContainer.innerHTML = myPosts.map(post => `
                    <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-4">
                        <p class="mb-4">${post.content}</p>
                        ${post.image ? `<img class="rounded-lg mb-4 max-h-40 w-auto mx-auto" src="${post.image}">` : ""}
                        <div class="flex space-x-4">
                            <span class="text-gray-500"><i class="fas fa-heart"></i> ${post.likes}</span>
                            <span class="text-gray-500"><i class="fas fa-comment"></i> ${app.getPostComments(post.id).length}</span>
                        </div>
                        <p class="text-xs text-gray-400 mt-2">${app.getFormattedTime(post.timestamp)}</p>
                    </div>
                `).join('');
            }
        }

        // 探索用戶
        function renderDiscover() {
            const users = Array.from(app.users.values());
            elements.discoverContainer.innerHTML = users.map(user => `
                <div class="bg-white dark:bg-gray-800 rounded-lg shadow-lg p-6 text-center">
                    <img class="w-20 h-20 rounded-full mx-auto mb-4" src="${user.avatar}">
                    <h3 class="text-lg font-bold mb-2">${user.username}</h3>
                    <p class="text-sm text-gray-500 mb-2">@${user.username}</p>
                    <p class="mb-4">${user.bio}</p>
                    <div class="flex justify-center space-x-4 mb-4">
                        <span class="text-gray-500"><i class="fas fa-user-friends"></i> ${user.followers.size} 粉絲</span>
                        <span class="text-gray-500"><i class="fas fa-edit"></i> ${user.postsCount} 發文</span>
                    </div>
                    <button class="follow-btn bg-primary hover:bg-primary-dark text-white px-4 py-2 rounded-lg" data-id="${user.id}">
                        ${app.isLoggedIn && app.isFollowing(app.currentUser.id, user.id) ? '已關注' : '關注'}
                    </button>
                </div>
            `).join('');
        }
        elements.discoverContainer.addEventListener('click', function(e) {
            if (e.target.closest('.follow-btn')) {
                const btn = e.target.closest('.follow-btn');
                const userId = parseInt(btn.dataset.id);
                if (!app.isLoggedIn) {
                    openAuthModal('login');
                    return;
                }
                if (app.isFollowing(app.currentUser.id, userId)) {
                    app.unfollowUser(app.currentUser.id, userId);
                } else {
                    app.followUser(app.currentUser.id, userId);
                }
                renderDiscover();
                renderSidebar();
            }
        });

        // 通知
        function renderNotifications() {
            if (!app.isLoggedIn) {
                elements.notificationsContainer.innerHTML = "<div class='p-6 text-center'>請登入以查看通知</div>";
                elements.notificationBadge.textContent = "0";
                return;
            }
            const notifications = app.notifications.filter(n => n.toUserId === app.currentUser.id);
            elements.notificationsContainer.innerHTML = notifications.map(notif => {
                const fromUser = app.users.get(notif.fromUserId);
                return `
                    <div class="flex items-center px-6 py-4">
                        <img class="w-10 h-10 rounded-full mr-3" src="${fromUser?.avatar || ''}">
                        <div>
                            <p class="font-bold">${fromUser?.username || '系統'}</p>
                            <p>${notif.message}</p>
                            <p class="text-xs text-gray-500">${app.getFormattedTime(notif.timestamp)}</p>
                        </div>
                    </div>
                `;
            }).join('');
            const unread = notifications.filter(n => !n.read).length;
            elements.notificationBadge.textContent = unread;
        }

        // 評論 Modal
        function renderComments(postId) {
            elements.commentModal.classList.remove('hidden');
            const post = app.posts.find(p => p.id === postId);
            const user = app.users.get(post.userId);
            const comments = app.getPostComments(postId);
            elements.commentContent.innerHTML = `
                <div class="mb-6">
                    <div class="flex items-center mb-2">
                        <img class="w-8 h-8 rounded-full mr-2" src="${user.avatar}">
                        <span class="font-bold">${user.username}</span>
                        <span class="ml-2 text-xs text-gray-500">${app.getFormattedTime(post.timestamp)}</span>
                    </div>
                    <p>${post.content}</p>
                </div>
                <div class="mb-6">
                    <h4 class="font-bold mb-2">評論</h4>
                    <div>${comments.map(cmt => {
                        const cu = app.users.get(cmt.userId);
                        return `
                            <div class="flex items-center mb-2">
                                <img class="w-6 h-6 rounded-full mr-2" src="${cu.avatar}">
                                <span class="font-semibold">${cu.username}</span>
                                <span class="ml-2 text-xs text-gray-500">${app.getFormattedTime(cmt.timestamp)}</span>
                            </div>
                            <p class="mb-2">${cmt.content}</p>
                        `;
                    }).join('')}</div>
                </div>
                ${app.isLoggedIn ? `
                    <form id="comment-form">
                        <textarea id="comment-input" class="w-full p-2 border border-gray-300 dark:border-gray-600 rounded-lg focus:outline-none focus:ring-2 focus:ring-primary resize-none text-base bg-white dark:bg-gray-700 mb-2" rows="2" placeholder="寫下評論..."></textarea>
                        <button type="submit" class="bg-primary hover:bg-primary-dark text-white px-4 py-2 rounded-lg">發布</button>
                    </form>
                ` : `<div class="text-center text-gray-500">請登入以發表評論</div>`}
            `;
            // 評論提交
            const form = document.getElementById('comment-form');
            if (form) {
                form.addEventListener('submit', function(e) {
                    e.preventDefault();
                    const content = document.getElementById('comment-input').value;
                    if (content.trim() === "") return;
                    app.addComment(postId, app.currentUser.id, content);
                    renderComments(postId);
                    renderPosts();
                });
            }
        }
        elements.closeCommentModal.addEventListener('click', () => {
            elements.commentModal.classList.add('hidden');
        });

        // 關閉用戶資料 Modal
        elements.closeUserProfileModal.addEventListener('click', () => {
            elements.userProfileModal.classList.add('hidden');
        });

        // 首次渲染
        showTab('home');
        renderSidebar();
        renderPosts();
    </script>
</body>
</html>
