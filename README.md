<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>NoteSpark AI - Complete Student Learning Platform</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;500;600;700&display=swap" rel="stylesheet">
    <script src="https://cdn.tailwindcss.com"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/three.js/r128/three.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/axios/dist/axios.min.js"></script>
    <style>
        :root {
            --primary-indigo: #6366F1;
            --primary-emerald: #10B981;
            --glow-color: rgba(99, 102, 241, 0.5);
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Inter', sans-serif;
        }
        
        body {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            color: #f8fafc;
            overflow-x: hidden;
        }
        
        /* Space Background */
        .space-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -10;
            background: radial-gradient(ellipse at bottom, #1B2735 0%, #090A0F 100%);
        }
        
        .stars {
            position: absolute;
            top: 50%;
            left: 50%;
            width: 1px;
            height: 1px;
            background: transparent;
            border-radius: 50%;
            animation: zoom 20s alternate infinite;
        }
        
        .stars1 {
            box-shadow: -24vw -44vh 2px 2px #fff, 38vw -4vh 0px 0px #fff, -20vw -48vh 1px 2px #fff, -39vw 38vh 3px 1px #fff, -42vw -11vh 0px 3px #fff, 12vw 15vh 3px 3px #fff, 42vw 6vh 3px 2px #fff, -8vw 9vh 0px 2px #fff, 34vw -38vh 1px 0px #fff, -17vw 45vh 3px 1px #fff, 22vw -36vh 3px 2px #fff, -42vw 1vh 1px 0px #fff;
            animation-duration: 25s;
        }
        
        .stars2 {
            box-shadow: 15vw -30vh 1px 1px #fff, -22vw 18vh 1px 1px #fff, 45vw 15vh 2px 0px #fff, -15vw -25vh 1px 1px #aaf, 30vw 40vh 1px 1px #aaf, -40vw -15vh 2px 1px #aaf;
            animation-duration: 30s;
            animation-delay: -5s;
        }
        
        .stars3 {
            box-shadow: -5vw -15vh 1px 0px #fff, 25vw 35vh 1px 0px #fff, -35vw 5vh 1px 0px #aaf, 18vw -8vh 1px 0px #aaf, -28vw -32vh 1px 0px #aaf, 8vw 22vh 1px 0px #aaf;
            animation-duration: 35s;
            animation-delay: -10s;
        }
        
        @keyframes zoom {
            0% { transform: scale(1); }
            100% { transform: scale(1.8); }
        }
        
        .shooting-star {
            position: absolute;
            top: 0;
            left: 0;
            width: 2px;
            height: 2px;
            background: linear-gradient(45deg, white, transparent);
            border-radius: 50%;
            opacity: 0;
            box-shadow: 0 0 10px 2px white;
        }
        
        /* Animations */
        .glow-effect {
            box-shadow: 
                0 0 20px rgba(99, 102, 241, 0.3),
                0 0 40px rgba(99, 102, 241, 0.2),
                0 0 60px rgba(99, 102, 241, 0.1);
            animation: pulse-glow 2s infinite alternate;
        }
        
        @keyframes pulse-glow {
            from { opacity: 0.7; }
            to { opacity: 1; }
        }
        
        .floating {
            animation: floating 3s ease-in-out infinite;
        }
        
        @keyframes floating {
            0% { transform: translate(0, 0px); }
            50% { transform: translate(0, -15px); }
            100% { transform: translate(0, 0px); }
        }
        
        .card-hover {
            transition: all 0.3s ease;
        }
        
        .card-hover:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.3), 0 10px 10px -5px rgba(0, 0, 0, 0.1);
        }
        
        .sidebar-icon {
            transition: all 0.3s ease;
        }
        
        .sidebar-icon:hover {
            transform: scale(1.1);
            filter: drop-shadow(0 0 8px var(--primary-indigo));
        }
        
        .flip-card {
            perspective: 1000px;
        }
        
        .flip-card-inner {
            transition: transform 0.6s;
            transform-style: preserve-3d;
        }
        
        .flip-card:hover .flip-card-inner {
            transform: rotateY(180deg);
        }
        
        .flip-card-front, .flip-card-back {
            backface-visibility: hidden;
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
        }
        
        .flip-card-back {
            transform: rotateY(180deg);
        }
        
        .progress-bar {
            height: 8px;
            border-radius: 4px;
            background: #334155;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            border-radius: 4px;
            background: linear-gradient(90deg, var(--primary-indigo), var(--primary-emerald));
            transition: width 0.5s ease;
        }
        
        .typewriter {
            overflow: hidden;
            border-right: 2px solid var(--primary-indigo);
            white-space: nowrap;
            animation: typing 3.5s steps(40, end), blink-caret 0.75s step-end infinite;
        }
        
        @keyframes typing {
            from { width: 0 }
            to { width: 100% }
        }
        
        @keyframes blink-caret {
            from, to { border-color: transparent }
            50% { border-color: var(--primary-indigo) }
        }
        
        .particle {
            position: absolute;
            border-radius: 50%;
            background: rgba(99, 102, 241, 0.5);
            animation: float-particle 15s infinite linear;
        }
        
        @keyframes float-particle {
            0% {
                transform: translateY(0) translateX(0);
                opacity: 0;
            }
            10% {
                opacity: 1;
            }
            90% {
                opacity: 1;
            }
            100% {
                transform: translateY(-100vh) translateX(100px);
                opacity: 0;
            }
        }
        
        /* Page Transitions */
        .page {
            display: none;
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        
        .page.active {
            display: block;
            opacity: 1;
        }
        
        /* Logo Animation */
        .logo-path {
            stroke-dasharray: 1000;
            stroke-dashoffset: 1000;
            animation: dash 5s ease-in-out forwards;
        }
        
        @keyframes dash {
            to {
                stroke-dashoffset: 0;
            }
        }
        
        /* Form Animations */
        .form-input {
            transition: all 0.3s ease;
        }
        
        .form-input:focus {
            transform: scale(1.02);
            box-shadow: 0 0 0 3px rgba(99, 102, 241, 0.3);
        }
        
        /* Sync Animation */
        .sync-pulse {
            animation: sync-pulse 2s infinite;
        }
        
        @keyframes sync-pulse {
            0% { transform: scale(1); opacity: 1; }
            50% { transform: scale(1.1); opacity: 0.7; }
            100% { transform: scale(1); opacity: 1; }
        }
        
        /* Loading Spinner */
        .spinner {
            border: 4px solid rgba(255, 255, 255, 0.3);
            border-radius: 50%;
            border-top: 4px solid #6366F1;
            width: 40px;
            height: 40px;
            animation: spin 1s linear infinite;
        }
        
        @keyframes spin {
            0% { transform: rotate(0deg); }
            100% { transform: rotate(360deg); }
        }
        
        /* Notification */
        .notification {
            position: fixed;
            top: 20px;
            right: 20px;
            padding: 15px 20px;
            border-radius: 8px;
            color: white;
            z-index: 1000;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
            transform: translateX(120%);
            transition: transform 0.3s ease;
        }
        
        .notification.show {
            transform: translateX(0);
        }
        
        .notification.success {
            background-color: #10B981;
        }
        
        .notification.error {
            background-color: #EF4444;
        }
        
        .notification.info {
            background-color: #6366F1;
        }
    </style>
</head>
<body class="min-h-screen text-white">
    <!-- Space Background -->
    <div class="space-bg">
        <div class="stars stars1"></div>
        <div class="stars stars2"></div>
        <div class="stars stars3"></div>
    </div>
    
    <!-- 3D Background Canvas -->
    <div id="threejs-background" class="fixed top-0 left-0 w-full h-full -z-10"></div>
    
    <!-- Notification System -->
    <div id="notification" class="notification"></div>
    
    <!-- Signup Page -->
    <div id="signup-page" class="page active min-h-screen flex items-center justify-center p-6">
        <div class="flex flex-col md:flex-row items-center justify-between">
            <div class="md:w-1/2 mb-10 md:mb-0">
                <!-- Enhanced Logo -->
                <div class="flex items-center space-x-3 mb-8">
                    <div class="relative">
                        <svg width="60" height="60" viewBox="0 0 60 60" class="glow-effect">
                            <defs>
                                <linearGradient id="logoGradient" x1="0%" y1="0%" x2="100%" y2="100%">
                                    <stop offset="0%" stop-color="#6366F1" />
                                    <stop offset="100%" stop-color="#10B981" />
                                </linearGradient>
                                <filter id="glow" x="-50%" y="-50%" width="200%" height="200%">
                                    <feGaussianBlur stdDeviation="4" result="coloredBlur"/>
                                    <feMerge> 
                                        <feMergeNode in="coloredBlur"/>
                                        <feMergeNode in="SourceGraphic"/>
                                    </feMerge>
                                </filter>
                            </defs>
                            <circle cx="30" cy="30" r="28" fill="url(#logoGradient)" filter="url(#glow)" />
                            <path class="logo-path" d="M20,20 L40,20 L40,40 L20,40 Z" fill="none" stroke="white" stroke-width="2" />
                            <path class="logo-path" d="M25,25 L35,35 M35,25 L25,35" stroke="white" stroke-width="2" />
                            <circle cx="30" cy="30" r="15" fill="none" stroke="white" stroke-width="2" />
                        </svg>
                    </div>
                    <h1 class="text-4xl font-bold bg-gradient-to-r from-indigo-400 to-emerald-400 bg-clip-text text-transparent">NoteSpark AI</h1>
                </div>
                
                <h1 class="text-5xl md:text-6xl font-bold mb-6 leading-tight">
                    <span class="typewriter">Transform Your</span>
                    <br>
                    <span class="bg-gradient-to-r from-indigo-400 to-emerald-400 bg-clip-text text-transparent">Learning Journey</span>
                </h1>
                <p class="text-xl text-gray-300 mb-8">
                    Study Smarter, Not Harder. Be part of a new generation of B.Tech students using AI to instantly create study guides, practice problems, and personalized progress reports.
                </p>
            </div>
            
            <div class="md:w-1/2 flex justify-center">
                <div class="relative w-full max-w-md">
                    <!-- Animated floating elements -->
                    <div class="absolute -top-10 -left-10 w-40 h-40 bg-indigo-500 rounded-full opacity-20 blur-xl floating"></div>
                    <div class="absolute -bottom-10 -right-10 w-40 h-40 bg-emerald-500 rounded-full opacity-20 blur-xl floating" style="animation-delay: 1.5s;"></div>
                    
                    <!-- Signup Form -->
                    <div class="bg-gray-800 bg-opacity-70 backdrop-blur-lg rounded-2xl p-8 border border-gray-700 glow-effect card-hover">
                        <h2 class="text-2xl font-bold mb-2 text-center">Create Your Account</h2>
                        <p class="text-gray-400 mb-6 text-center">Start your academic transformation today</p>
                        
                        <form id="signup-form" class="space-y-4">
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-sm font-medium mb-1">First Name</label>
                                    <input type="text" id="first-name" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                </div>
                                <div>
                                    <label class="block text-sm font-medium mb-1">Last Name</label>
                                    <input type="text" id="last-name" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium mb-1">Email</label>
                                <input type="email" id="email" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium mb-1">B.Tech Year</label>
                                <select id="year" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                    <option value="">Select Year</option>
                                    <option>1st Year</option>
                                    <option>2nd Year</option>
                                    <option>3rd Year</option>
                                    <option>4th Year</option>
                                </select>
                            </div>
                            
                            <div class="grid grid-cols-2 gap-4">
                                <div>
                                    <label class="block text-sm font-medium mb-1">Section</label>
                                    <select id="section" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                        <option value="">Select Section</option>
                                        <option>A</option>
                                        <option>B</option>
                                        <option>C</option>
                                        <option>D</option>
                                        <option>E</option>
                                        <option>F</option>
                                        <option>G</option>
                                        <option>H</option>
                                    </select>
                                </div>
                                <div>
                                    <label class="block text-sm font-medium mb-1">Group</label>
                                    <select id="group" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                        <option value="">Select Group</option>
                                        <option>A</option>
                                        <option>B</option>
                                    </select>
                                </div>
                            </div>
                            
                            <div>
                                <label class="block text-sm font-medium mb-1">Password</label>
                                <input type="password" id="password" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                <div class="text-xs text-gray-400 mt-1">Must be at least 8 characters with numbers and symbols</div>
                            </div>
                            
                            <div class="flex items-center">
                                <input type="checkbox" id="terms" required class="w-4 h-4 text-indigo-600 bg-gray-700 rounded focus:ring-indigo-500">
                                <label for="terms" class="ml-2 text-sm text-gray-300">I agree to the <a href="#" class="text-indigo-400 hover:text-indigo-300">Terms & Conditions</a></label>
                            </div>
                            
                            <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 py-3 rounded-lg font-semibold transition-all glow-effect flex justify-center items-center">
                                <span id="signup-text">Create Account</span>
                                <div id="signup-spinner" class="spinner ml-2 hidden"></div>
                            </button>
                        </form>
                        
                        <div class="mt-6 text-center text-sm text-gray-400">
                            Already have an account? <a href="#" id="show-login" class="text-indigo-400 hover:text-indigo-300 font-medium">Log In</a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Login Page -->
    <div id="login-page" class="page min-h-screen flex items-center justify-center p-6">
        <div class="max-w-md w-full">
            <div class="flex justify-center mb-8">
                <div class="flex items-center space-x-3">
                    <div class="relative">
                        <svg width="50" height="50" viewBox="0 0 50 50" class="glow-effect">
                            <circle cx="25" cy="25" r="23" fill="url(#logoGradient)" filter="url(#glow)" />
                            <path d="M15,15 L35,15 L35,35 L15,35 Z" fill="none" stroke="white" stroke-width="2" />
                            <path d="M20,20 L30,30 M30,20 L20,30" stroke="white" stroke-width="2" />
                            <circle cx="25" cy="25" r="12" fill="none" stroke="white" stroke-width="2" />
                        </svg>
                    </div>
                    <h1 class="text-3xl font-bold bg-gradient-to-r from-indigo-400 to-emerald-400 bg-clip-text text-transparent">NoteSpark AI</h1>
                </div>
            </div>
            
            <div class="bg-gray-800 bg-opacity-70 backdrop-blur-lg rounded-2xl p-8 border border-gray-700 glow-effect card-hover">
                <h2 class="text-2xl font-bold mb-2 text-center">Welcome Back</h2>
                <p class="text-gray-400 mb-6 text-center">Sign in to continue your learning journey</p>
                
                <form id="login-form" class="space-y-4">
                    <div>
                        <label class="block text-sm font-medium mb-1">Email</label>
                        <input type="email" id="login-email" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                    </div>
                    
                    <div>
                        <label class="block text-sm font-medium mb-1">Password</label>
                        <input type="password" id="login-password" required class="form-input w-full bg-gray-700 rounded-lg px-4 py-3 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                    </div>
                    
                    <div class="flex items-center justify-between">
                        <div class="flex items-center">
                            <input type="checkbox" id="remember" class="w-4 h-4 text-indigo-600 bg-gray-700 rounded focus:ring-indigo-500">
                            <label for="remember" class="ml-2 text-sm text-gray-300">Remember me</label>
                        </div>
                        <a href="#" class="text-sm text-indigo-400 hover:text-indigo-300">Forgot password?</a>
                    </div>
                    
                    <button type="submit" class="w-full bg-indigo-600 hover:bg-indigo-700 py-3 rounded-lg font-semibold transition-all glow-effect flex justify-center items-center">
                        <span id="login-text">Sign In</span>
                        <div id="login-spinner" class="spinner ml-2 hidden"></div>
                    </button>
                </form>
                
                <div class="mt-6 text-center text-sm text-gray-400">
                    Don't have an account? <a href="#" id="show-signup" class="text-indigo-400 hover:text-indigo-300 font-medium">Sign Up</a>
                </div>
            </div>
        </div>
    </div>
    
    <!-- Dashboard Page -->
    <div id="dashboard-page" class="page">
        <!-- Navigation Bar -->
        <nav class="flex justify-between items-center p-6 bg-gray-900 bg-opacity-70 backdrop-blur-lg border-b border-gray-800">
            <div class="flex items-center space-x-2">
                <div class="w-10 h-10 rounded-full bg-gradient-to-r from-indigo-500 to-emerald-500 flex items-center justify-center glow-effect">
                    <span id="user-initial" class="font-bold">E</span>
                </div>
                <h1 class="text-2xl font-bold bg-gradient-to-r from-indigo-400 to-emerald-400 bg-clip-text text-transparent">NoteSpark AI</h1>
            </div>
            
            <div class="hidden md:flex space-x-8">
                <a href="#features" class="text-gray-300 hover:text-white transition-colors">Features</a>
                <a href="#dashboard" class="text-gray-300 hover:text-white transition-colors">Dashboard</a>
                <a href="#ai-tools" class="text-gray-300 hover:text-white transition-colors">AI Tools</a>
                <a href="#support" class="text-gray-300 hover:text-white transition-colors">Support</a>
            </div>
            
            <div class="flex items-center space-x-4">
                <div class="flex items-center space-x-2 text-sm text-gray-300">
                    <div class="w-2 h-2 bg-green-500 rounded-full sync-pulse"></div>
                    <span id="sync-status">Synced</span>
                </div>
                <button id="logout-btn" class="px-4 py-2 bg-gray-800 rounded-lg font-medium hover:bg-gray-700 transition-all">
                    Logout
                </button>
            </div>
        </nav>

        <!-- Main Content -->
        <main class="container mx-auto px-4 py-8">
            <!-- Hero Section -->
            <section class="flex flex-col md:flex-row items-center justify-between py-16">
                <div class="md:w-1/2 mb-10 md:mb-0">
                    <h1 class="text-5xl md:text-6xl font-bold mb-6 leading-tight">
                        <span class="typewriter">Welcome to Your</span>
                        <br>
                        <span class="bg-gradient-to-r from-indigo-400 to-emerald-400 bg-clip-text text-transparent">Learning Dashboard</span>
                    </h1>
                    <p class="text-xl text-gray-300 mb-8">
                        Your personalized academic command center with AI-powered tools to excel in your B.Tech journey.
                    </p>
                    <div class="flex space-x-4">
                        <button id="upload-notes-btn" class="px-8 py-3 bg-gradient-to-r from-indigo-500 to-emerald-500 rounded-lg font-semibold text-lg hover:from-indigo-600 hover:to-emerald-600 transition-all glow-effect">
                            Upload Notes
                        </button>
                        <button id="generate-quiz-btn" class="px-8 py-3 bg-gray-800 rounded-lg font-semibold text-lg hover:bg-gray-700 transition-all border border-gray-700">
                            Generate Quiz
                        </button>
                    </div>
                </div>
                
                <div class="md:w-1/2 flex justify-center">
                    <div class="relative w-full max-w-lg">
                        <!-- 3D floating elements -->
                        <div class="absolute -top-10 -left-10 w-40 h-40 bg-indigo-500 rounded-full opacity-20 blur-xl floating"></div>
                        <div class="absolute -bottom-10 -right-10 w-40 h-40 bg-emerald-500 rounded-full opacity-20 blur-xl floating" style="animation-delay: 1.5s;"></div>
                        
                        <!-- Dashboard preview -->
                        <div class="bg-gray-800 bg-opacity-70 backdrop-blur-lg rounded-2xl p-6 border border-gray-700 glow-effect card-hover">
                            <div class="flex space-x-2 mb-4">
                                <div class="w-3 h-3 bg-red-500 rounded-full"></div>
                                <div class="w-3 h-3 bg-yellow-500 rounded-full"></div>
                                <div class="w-3 h-3 bg-green-500 rounded-full"></div>
                            </div>
                            
                            <div class="grid grid-cols-3 gap-4 mb-4">
                                <div class="bg-indigo-900 bg-opacity-50 p-3 rounded-lg border border-indigo-800">
                                    <div class="text-xs text-indigo-300 mb-1">Notes</div>
                                    <div id="notes-count" class="font-bold">24</div>
                                </div>
                                <div class="bg-emerald-900 bg-opacity-50 p-3 rounded-lg border border-emerald-800">
                                    <div class="text-xs text-emerald-300 mb-1">Quizzes</div>
                                    <div id="quizzes-count" class="font-bold">12</div>
                                </div>
                                <div class="bg-purple-900 bg-opacity-50 p-3 rounded-lg border border-purple-800">
                                    <div class="text-xs text-purple-300 mb-1">Rank</div>
                                    <div id="user-rank" class="font-bold">#8</div>
                                </div>
                            </div>
                            
                            <div class="bg-gray-900 p-4 rounded-lg">
                                <div class="flex justify-between mb-2">
                                    <span class="text-sm">AI Quiz Progress</span>
                                    <span class="text-sm font-bold">65%</span>
                                </div>
                                <div class="progress-bar">
                                    <div class="progress-fill" style="width: 65%"></div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Features Section -->
            <section id="features" class="py-16">
                <h2 class="text-4xl font-bold text-center mb-4">Powerful Learning Features</h2>
                <p class="text-xl text-gray-400 text-center mb-12 max-w-3xl mx-auto">
                    Everything you need to excel in your B.Tech journey, powered by advanced AI technology
                </p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                    <!-- Feature 1 -->
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 border border-gray-700 card-hover">
                        <div class="w-14 h-14 rounded-lg bg-indigo-900 bg-opacity-50 flex items-center justify-center mb-4 glow-effect">
                            <svg class="w-7 h-7 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Smart Notes System</h3>
                        <p class="text-gray-300 mb-4">
                            Upload, organize, and share notes with AI-powered categorization and OCR for handwritten content.
                        </p>
                        <ul class="text-sm text-gray-400 space-y-1">
                            <li>• Drag & drop file upload</li>
                            <li>• Automatic topic tagging</li>
                            <li>• Collaborative editing</li>
                        </ul>
                    </div>
                    
                    <!-- Feature 2 -->
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 border border-gray-700 card-hover">
                        <div class="w-14 h-14 rounded-lg bg-emerald-900 bg-opacity-50 flex items-center justify-center mb-4 glow-effect">
                            <svg class="w-7 h-7 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">AI Quiz Generator</h3>
                        <p class="text-gray-300 mb-4">
                            Generate custom quizzes from your notes and previous year papers with adaptive difficulty.
                        </p>
                        <ul class="text-sm text-gray-400 space-y-1">
                            <li>• Context-aware questions</li>
                            <li>• Multiple question types</li>
                            <li>• Performance analytics</li>
                        </ul>
                    </div>
                    
                    <!-- Feature 3 -->
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 border border-gray-700 card-hover">
                        <div class="w-14 h-14 rounded-lg bg-purple-900 bg-opacity-50 flex items-center justify-center mb-4 glow-effect">
                            <svg class="w-7 h-7 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Social Learning</h3>
                        <p class="text-gray-300 mb-4">
                            Connect with classmates, form study groups, and share resources in a collaborative environment.
                        </p>
                        <ul class="text-sm text-gray-400 space-y-1">
                            <li>• Peer connections</li>
                            <li>• Study groups</li>
                            <li>• Resource sharing</li>
                        </ul>
                    </div>
                </div>
            </section>

            <!-- Dashboard Preview -->
            <section id="dashboard" class="py-16 bg-gray-800 bg-opacity-30 rounded-2xl p-8 my-8">
                <h2 class="text-4xl font-bold text-center mb-4">Interactive Learning Dashboard</h2>
                <p class="text-xl text-gray-400 text-center mb-12 max-w-3xl mx-auto">
                    Your personalized academic command center with all the tools you need
                </p>
                
                <div class="bg-gray-900 rounded-2xl overflow-hidden border border-gray-700">
                    <!-- Dashboard Header -->
                    <div class="flex justify-between items-center p-4 bg-gray-800 border-b border-gray-700">
                        <div class="flex items-center space-x-4">
                            <div class="flex space-x-1">
                                <div class="w-3 h-3 bg-red-500 rounded-full"></div>
                                <div class="w-3 h-3 bg-yellow-500 rounded-full"></div>
                                <div class="w-3 h-3 bg-green-500 rounded-full"></div>
                            </div>
                            <div class="text-sm font-medium">NoteSpark AI Dashboard</div>
                        </div>
                        <div class="flex items-center space-x-4">
                            <div class="flex items-center space-x-2 bg-gray-700 px-3 py-1 rounded-lg">
                                <div class="w-2 h-2 bg-green-500 rounded-full"></div>
                                <span class="text-sm">Online</span>
                            </div>
                            <div class="w-8 h-8 bg-indigo-600 rounded-full flex items-center justify-center">
                                <span id="user-initial-small" class="text-xs font-bold">JS</span>
                            </div>
                        </div>
                    </div>
                    
                    <!-- Dashboard Content -->
                    <div class="flex">
                        <!-- Sidebar -->
                        <div class="w-20 bg-gray-800 border-r border-gray-700 py-4 flex flex-col items-center">
                            <div class="sidebar-icon mb-6 p-3 rounded-lg bg-indigo-900 bg-opacity-50 glow-effect">
                                <svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6"></path>
                                </svg>
                            </div>
                            
                            <div class="sidebar-icon mb-4 p-3 rounded-lg hover:bg-gray-700">
                                <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                                </svg>
                            </div>
                            
                            <div class="sidebar-icon mb-4 p-3 rounded-lg hover:bg-gray-700">
                                <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5H7a2 2 0 00-2 2v12a2 2 0 002 2h10a2 2 0 002-2V7a2 2 0 00-2-2h-2M9 5a2 2 0 002 2h2a2 2 0 002-2M9 5a2 2 0 012-2h2a2 2 0 012 2"></path>
                                </svg>
                            </div>
                            
                            <div class="sidebar-icon mb-4 p-3 rounded-lg hover:bg-gray-700">
                                <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
                                </svg>
                            </div>
                            
                            <div class="sidebar-icon mb-4 p-3 rounded-lg hover:bg-gray-700">
                                <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z"></path>
                                </svg>
                            </div>
                            
                            <div class="sidebar-icon mt-auto p-3 rounded-lg hover:bg-gray-700">
                                <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10.325 4.317c.426-1.756 2.924-1.756 3.35 0a1.724 1.724 0 002.573 1.066c1.543-.94 3.31.826 2.37 2.37a1.724 1.724 0 001.065 2.572c1.756.426 1.756 2.924 0 3.35a1.724 1.724 0 00-1.066 2.573c.94 1.543-.826 3.31-2.37 2.37a1.724 1.724 0 00-2.572 1.065c-.426 1.756-2.924 1.756-3.35 0a1.724 1.724 0 00-2.573-1.066c-1.543.94-3.31-.826-2.37-2.37a1.724 1.724 0 00-1.065-2.572c-1.756-.426-1.756-2.924 0-3.35a1.724 1.724 0 001.066-2.573c-.94-1.543.826-3.31 2.37-2.37.996.608 2.296.07 2.572-1.065z"></path>
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z"></path>
                                </svg>
                            </div>
                        </div>
                        
                        <!-- Main Content -->
                        <div class="flex-1 p-6">
                            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                                <!-- Notes Card -->
                                <div class="bg-gray-800 rounded-xl p-4 border border-gray-700 card-hover">
                                    <div class="flex justify-between items-center mb-4">
                                        <h3 class="font-bold text-lg">My Notes</h3>
                                        <span class="text-xs bg-indigo-900 text-indigo-300 px-2 py-1 rounded-full" id="notes-count-small">24 files</span>
                                    </div>
                                    <div id="notes-list" class="space-y-3">
                                        <!-- Notes will be dynamically loaded here -->
                                    </div>
                                    <button id="upload-new-notes" class="w-full mt-4 py-2 bg-gray-700 hover:bg-gray-600 rounded-lg text-sm font-medium transition-colors">
                                        Upload New Notes
                                    </button>
                                </div>
                                
                                <!-- Quiz Card -->
                                <div class="bg-gray-800 rounded-xl p-4 border border-gray-700 card-hover">
                                    <div class="flex justify-between items-center mb-4">
                                        <h3 class="font-bold text-lg">AI Quiz Generator</h3>
                                        <span class="text-xs bg-emerald-900 text-emerald-300 px-2 py-1 rounded-full">New</span>
                                    </div>
                                    <p class="text-gray-400 text-sm mb-4">
                                        Generate custom quizzes from your notes and previous year papers
                                    </p>
                                    <div class="space-y-3 mb-4">
                                        <div class="flex items-center justify-between">
                                            <span class="text-sm">From Notes</span>
                                            <button id="generate-from-notes" class="px-3 py-1 bg-indigo-600 hover:bg-indigo-700 rounded-lg text-xs font-medium transition-colors">
                                                Generate
                                            </button>
                                        </div>
                                        <div class="flex items-center justify-between">
                                            <span class="text-sm">From PYQs</span>
                                            <button id="generate-from-pyqs" class="px-3 py-1 bg-indigo-600 hover:bg-indigo-700 rounded-lg text-xs font-medium transition-colors">
                                                Generate
                                            </button>
                                        </div>
                                    </div>
                                    <div class="bg-gray-900 p-3 rounded-lg">
                                        <div class="flex justify-between mb-1">
                                            <span class="text-xs">Quiz Completion</span>
                                            <span class="text-xs font-bold">65%</span>
                                        </div>
                                        <div class="progress-bar">
                                            <div class="progress-fill" style="width: 65%"></div>
                                        </div>
                                    </div>
                                </div>
                                
                                <!-- Progress Card -->
                                <div class="bg-gray-800 rounded-xl p-4 border border-gray-700 card-hover">
                                    <div class="flex justify-between items-center mb-4">
                                        <h3 class="font-bold text-lg">My Progress</h3>
                                        <span class="text-xs bg-purple-900 text-purple-300 px-2 py-1 rounded-full" id="user-rank-small">Rank #8</span>
                                    </div>
                                    <div class="space-y-4">
                                        <div>
                                            <div class="flex justify-between mb-1">
                                                <span class="text-sm">Notes Mastery</span>
                                                <span class="text-sm font-bold">78%</span>
                                            </div>
                                            <div class="progress-bar">
                                                <div class="progress-fill" style="width: 78%"></div>
                                            </div>
                                        </div>
                                        <div>
                                            <div class="flex justify-between mb-1">
                                                <span class="text-sm">Quiz Performance</span>
                                                <span class="text-sm font-bold">65%</span>
                                            </div>
                                            <div class="progress-bar">
                                                <div class="progress-fill" style="width: 65%"></div>
                                            </div>
                                        </div>
                                        <div>
                                            <div class="flex justify-between mb-1">
                                                <span class="text-sm">Task Completion</span>
                                                <span class="text-sm font-bold">42%</span>
                                            </div>
                                            <div class="progress-bar">
                                                <div class="progress-fill" style="width: 42%"></div>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- AI Tools Section -->
            <section id="ai-tools" class="py-16">
                <h2 class="text-4xl font-bold text-center mb-4">Advanced AI Learning Tools</h2>
                <p class="text-xl text-gray-400 text-center mb-12 max-w-3xl mx-auto">
                    Harness the power of artificial intelligence to enhance your learning experience
                </p>
                
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-12 items-center">
                    <div>
                        <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-2xl p-6 border border-gray-700 mb-8 card-hover">
                            <div class="flex items-center mb-4">
                                <div class="w-12 h-12 rounded-lg bg-indigo-900 bg-opacity-50 flex items-center justify-center mr-4 glow-effect">
                                    <svg class="w-6 h-6 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                                    </svg>
                                </div>
                                <h3 class="text-2xl font-bold">AI Quiz Generation</h3>
                            </div>
                            <p class="text-gray-300 mb-4">
                                Our advanced AI analyzes your notes and previous year papers to create personalized quizzes that adapt to your learning level.
                            </p>
                            <ul class="text-gray-400 space-y-2">
                                <li>• Context-aware question generation from your materials</li>
                                <li>• Adaptive difficulty based on your performance</li>
                                <li>• Detailed explanations for each answer</li>
                                <li>• Identify and focus on your weak areas</li>
                            </ul>
                        </div>
                        
                        <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-2xl p-6 border border-gray-700 card-hover">
                            <div class="flex items-center mb-4">
                                <div class="w-12 h-12 rounded-lg bg-emerald-900 bg-opacity-50 flex items-center justify-center mr-4 glow-effect">
                                    <svg class="w-6 h-6 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9.663 17h4.673M12 3v1m6.364 1.636l-.707.707M21 12h-1M4 12H3m3.343-5.657l-.707-.707m2.828 9.9a5 5 0 117.072 0l-.548.547A3.374 3.374 0 0014 18.469V19a2 2 0 11-4 0v-.531c0-.895-.356-1.754-.988-2.386l-.548-.547z"></path>
                                    </svg>
                                </div>
                                <h3 class="text-2xl font-bold">Smart Study Assistant</h3>
                            </div>
                            <p class="text-gray-300 mb-4">
                                Get instant help with difficult concepts, generate study plans, and receive personalized resource recommendations.
                            </p>
                            <ul class="text-gray-400 space-y-2">
                                <li>• 24/7 doubt resolution and concept explanation</li>
                                <li>• Personalized study plan generation</li>
                                <li>• Voice interaction support</li>
                                <li>• Resource recommendations based on your needs</li>
                            </ul>
                        </div>
                    </div>
                    
                    <div class="flex justify-center">
                        <div class="relative w-full max-w-md">
                            <!-- 3D floating elements -->
                            <div class="absolute -top-10 -left-10 w-32 h-32 bg-indigo-500 rounded-full opacity-20 blur-xl floating"></div>
                            <div class="absolute -bottom-10 -right-10 w-32 h-32 bg-emerald-500 rounded-full opacity-20 blur-xl floating" style="animation-delay: 1.5s;"></div>
                            
                            <!-- AI Chat Preview -->
                            <div class="bg-gray-800 rounded-2xl p-6 border border-gray-700 glow-effect">
                                <div class="flex items-center mb-6">
                                    <div class="w-10 h-10 rounded-full bg-gradient-to-r from-indigo-500 to-emerald-500 flex items-center justify-center mr-3">
                                        <span class="font-bold text-white">AI</span>
                                    </div>
                                    <div>
                                        <div class="font-bold">Study Assistant</div>
                                        <div class="text-xs text-green-400">Online</div>
                                    </div>
                                </div>
                                
                                <div id="ai-chat" class="space-y-4 mb-6 max-h-60 overflow-y-auto">
                                    <!-- AI Chat messages will be dynamically added here -->
                                </div>
                                
                                <div class="flex">
                                    <input type="text" id="ai-chat-input" placeholder="Ask me anything..." class="flex-1 bg-gray-700 rounded-l-lg px-4 py-2 text-sm focus:outline-none focus:ring-2 focus:ring-indigo-500">
                                    <button id="ai-chat-send" class="bg-indigo-600 hover:bg-indigo-700 px-4 rounded-r-lg transition-colors">
                                        <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3"></path>
                                        </svg>
                                    </button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Support Section -->
            <section id="support" class="py-16">
                <h2 class="text-4xl font-bold text-center mb-4">Help & Support</h2>
                <p class="text-xl text-gray-400 text-center mb-12 max-w-3xl mx-auto">
                    We're here to help you succeed. Multiple support channels available.
                </p>
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8">
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 text-center border border-gray-700 card-hover">
                        <div class="w-16 h-16 rounded-full bg-indigo-900 bg-opacity-50 flex items-center justify-center mx-auto mb-4 glow-effect">
                            <svg class="w-8 h-8 text-indigo-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 10h.01M12 10h.01M16 10h.01M9 16H5a2 2 0 01-2-2V6a2 2 0 012-2h14a2 2 0 012 2v8a2 2 0 01-2 2h-5l-5 5v-5z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">AI Help Bot</h3>
                        <p class="text-gray-300 mb-4">
                            Instant answers to common queries 24/7
                        </p>
                        <button id="ai-help-chat" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 rounded-lg text-sm font-medium transition-colors">
                            Chat Now
                        </button>
                    </div>
                    
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 text-center border border-gray-700 card-hover">
                        <div class="w-16 h-16 rounded-full bg-emerald-900 bg-opacity-50 flex items-center justify-center mx-auto mb-4 glow-effect">
                            <svg class="w-8 h-8 text-emerald-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 5a2 2 0 012-2h3.28a1 1 0 01.948.684l1.498 4.493a1 1 0 01-.502 1.21l-2.257 1.13a11.042 11.042 0 005.516 5.516l1.13-2.257a1 1 0 011.21-.502l4.493 1.498a1 1 0 01.684.949V19a2 2 0 01-2 2h-1C9.716 21 3 14.284 3 6V5z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Help Line</h3>
                        <p class="text-gray-300 mb-4">
                            Direct support during business hours
                        </p>
                        <div class="text-emerald-400 font-bold">+91 9569370151</div>
                        <h3 class="text-sm mt-2">For any suggestion</h3>
                        <h3 class="text-sm">Email: aryanshukla1918@gmail.com</h3>
                    </div>
                    
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 text-center border border-gray-700 card-hover">
                        <div class="w-16 h-16 rounded-full bg-purple-900 bg-opacity-50 flex items-center justify-center mx-auto mb-4 glow-effect">
                            <svg class="w-8 h-8 text-purple-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12l2 2 4-4m5.618-4.016A11.955 11.955 0 0112 2.944a11.955 11.955 0 01-8.618 3.04A12.02 12.02 0 003 9c0 5.591 3.824 10.29 9 11.622 5.176-1.332 9-6.03 9-11.622 0-1.042-.133-2.052-.382-3.016z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Video Tutorials</h3>
                        <p class="text-gray-300 mb-4">
                            Step-by-step platform usage guides
                        </p>
                        <button id="video-tutorials" class="px-4 py-2 bg-purple-600 hover:bg-purple-700 rounded-lg text-sm font-medium transition-colors">
                            Watch Now
                        </button>
                    </div>
                    
                    <div class="bg-gray-800 bg-opacity-50 backdrop-blur-lg rounded-xl p-6 text-center border border-gray-700 card-hover">
                        <div class="w-16 h-16 rounded-full bg-amber-900 bg-opacity-50 flex items-center justify-center mx-auto mb-4 glow-effect">
                            <svg class="w-8 h-8 text-amber-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 11a7 7 0 01-7 7m0 0a7 7 0 01-7-7m7 7v4m0 0H8m4 0h4m-4-8a3 3 0 01-3-3V5a3 3 0 116 0v6a3 3 0 01-3 3z"></path>
                            </svg>
                        </div>
                        <h3 class="text-xl font-bold mb-2">Suggestions</h3>
                        <p class="text-gray-300 mb-4">
                            We value your feedback and ideas
                        </p>
                        <button id="suggestions-btn" class="px-4 py-2 bg-amber-600 hover:bg-amber-700 rounded-lg text-sm font-medium transition-colors">
                            Share Ideas
                        </button>
                    </div>
                </div>
            </section>
        </main>

        <!-- Footer -->
        <footer class="bg-gray-900 border-t border-gray-800 py-12">
            <div class="container mx-auto px-4">
                <div class="grid grid-cols-1 md:grid-cols-4 gap-8">
                    <div>
                        <div class="flex items-center space-x-2 mb-4">
                            <div class="w-8 h-8 rounded-full bg-gradient-to-r from-indigo-500 to-emerald-500 flex items-center justify-center">
                                <span class="font-bold text-white text-sm">E</span>
                            </div>
                            <h2 class="text-xl font-bold">NoteSpark AI</h2>
                        </div>
                        <p class="text-gray-400 text-sm">
                            Revolutionizing B.Tech education through AI-powered learning tools and collaborative platforms.
                        </p>
                    </div>
                    
                    <div>
                        <h3 class="font-bold text-lg mb-4">STUDY</h3>
                        <ul class="space-y-2 text-gray-400">
                            <li><a href="#" class="hover:text-white transition-colors">Features</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Details</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Case Studies</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Updates</a></li>
                        </ul>
                    </div>
                    
                    <div>
                        <h3 class="font-bold text-lg mb-4">Company</h3>
                        <ul class="space-y-2 text-gray-400">
                            <li><a href="#" class="hover:text-white transition-colors">About</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Careers</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Contact</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Blog</a></li>
                        </ul>
                    </div>
                    
                    <div>
                        <h3 class="font-bold text-lg mb-4">Legal</h3>
                        <ul class="space-y-2 text-gray-400">
                            <li><a href="#" class="hover:text-white transition-colors">Terms</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Privacy</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Cookies</a></li>
                            <li><a href="#" class="hover:text-white transition-colors">Licenses</a></li>
                        </ul>
                    </div>
                </div>
                
                <div class="border-t border-gray-800 mt-8 pt-8 text-center text-gray-500 text-sm">
                    <p> @ 2025 thanks for connecting us...</p>
                </div>
            </div>
        </footer>
    </div>

    <!-- File Upload Modal -->
    <div id="upload-modal" class="fixed inset-0 bg-black bg-opacity-70 flex items-center justify-center z-50 hidden">
        <div class="bg-gray-800 rounded-2xl p-8 max-w-md w-full mx-4 border border-gray-700">
            <div class="flex justify-between items-center mb-6">
                <h3 class="text-xl font-bold">Upload Notes</h3>
                <button id="close-upload-modal" class="text-gray-400 hover:text-white">
                    <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12"></path>
                    </svg>
                </button>
            </div>
            
            <div class="border-2 border-dashed border-gray-600 rounded-lg p-8 text-center mb-6">
                <svg class="w-12 h-12 text-gray-400 mx-auto mb-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                </svg>
                <p class="text-gray-400 mb-2">Drag & drop files here</p>
                <p class="text-gray-500 text-sm">or</p>
                <input type="file" id="file-input" class="hidden" multiple>
                <label for="file-input" class="inline-block mt-2 px-4 py-2 bg-indigo-600 hover:bg-indigo-700 rounded-lg text-sm font-medium cursor-pointer">
                    Browse Files
                </label>
            </div>
            
            <div id="selected-files" class="mb-6 max-h-40 overflow-y-auto hidden">
                <h4 class="text-sm font-medium mb-2">Selected Files:</h4>
                <div id="file-list" class="space-y-2"></div>
            </div>
            
            <div class="flex justify-end space-x-3">
                <button id="cancel-upload" class="px-4 py-2 bg-gray-700 hover:bg-gray-600 rounded-lg">
                    Cancel
                </button>
                <button id="confirm-upload" class="px-4 py-2 bg-indigo-600 hover:bg-indigo-700 rounded-lg">
                    Upload
                </button>
            </div>
        </div>
    </div>

    <script>
        // Backend API URL - Replace with your actual backend URL
        const API_BASE_URL = 'https://your-backend-domain.com/api';
        
        // Mock backend simulation - In a real implementation, this would be replaced with actual API calls
        class BackendAPI {
            constructor() {
                this.users = JSON.parse(localStorage.getItem('NoteSparkUsers')) || {};
                this.notes = JSON.parse(localStorage.getItem('NoteSparkNotes')) || {};
                this.quizzes = JSON.parse(localStorage.getItem('NoteSparkQuizzes')) || {};
                this.chats = JSON.parse(localStorage.getItem('NoteSparkChats')) || {};
            }
            
            // User Authentication
            async signup(userData) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        if (this.users[userData.email]) {
                            reject({ message: 'User already exists with this email' });
                        } else {
                            const userId = Date.now().toString();
                            const user = {
                                id: userId,
                                ...userData,
                                createdAt: new Date().toISOString(),
                                updatedAt: new Date().toISOString()
                            };
                            
                            this.users[userData.email] = user;
                            localStorage.setItem('NoteSparkUsers', JSON.stringify(this.users));
                            
                            // Initialize user data
                            this.notes[userId] = [];
                            this.quizzes[userId] = [];
                            this.chats[userId] = [];
                            
                            localStorage.setItem('NoteSparkNotes', JSON.stringify(this.notes));
                            localStorage.setItem('NoteSparkQuizzes', JSON.stringify(this.quizzes));
                            localStorage.setItem('NoteSparkChats', JSON.stringify(this.chats));
                            
                            resolve({ 
                                success: true, 
                                user: { 
                                    id: userId,
                                    firstName: userData.firstName,
                                    lastName: userData.lastName,
                                    email: userData.email
                                } 
                            });
                        }
                    }, 1000);
                });
            }
            
            async login(email, password) {
                return new Promise((resolve, reject) => {
                    setTimeout(() => {
                        const user = this.users[email];
                        if (user && user.password === password) {
                            resolve({ 
                                success: true, 
                                user: { 
                                    id: user.id,
                                    firstName: user.firstName,
                                    lastName: user.lastName,
                                    email: user.email
                                } 
                            });
                        } else {
                            reject({ message: 'Invalid email or password' });
                        }
                    }, 1000);
                });
            }
            
            // Notes Management
            async getNotes(userId) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(this.notes[userId] || []);
                    }, 500);
                });
            }
            
            async addNote(userId, noteData) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        const noteId = Date.now().toString();
                        const note = {
                            id: noteId,
                            ...noteData,
                            createdAt: new Date().toISOString()
                        };
                        
                        if (!this.notes[userId]) {
                            this.notes[userId] = [];
                        }
                        
                        this.notes[userId].push(note);
                        localStorage.setItem('NoteSparkNotes', JSON.stringify(this.notes));
                        
                        resolve({ success: true, note });
                    }, 800);
                });
            }
            
            async deleteNote(userId, noteId) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        if (this.notes[userId]) {
                            this.notes[userId] = this.notes[userId].filter(note => note.id !== noteId);
                            localStorage.setItem('NoteSparkNotes', JSON.stringify(this.notes));
                        }
                        resolve({ success: true });
                    }, 500);
                });
            }
            
            // Quiz Management
            async generateQuiz(userId, type, source) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        const quizId = Date.now().toString();
                        const quiz = {
                            id: quizId,
                            type,
                            source,
                            title: `${type} Quiz from ${source}`,
                            questions: [
                                {
                                    id: 1,
                                    question: "What is the time complexity of binary search?",
                                    options: ["O(1)", "O(log n)", "O(n)", "O(n log n)"],
                                    correctAnswer: 1
                                },
                                {
                                    id: 2,
                                    question: "Which data structure uses LIFO principle?",
                                    options: ["Queue", "Stack", "Array", "Linked List"],
                                    correctAnswer: 1
                                },
                                {
                                    id: 3,
                                    question: "What is the full form of HTML?",
                                    options: [
                                        "Hyper Text Markup Language",
                                        "High Tech Modern Language",
                                        "Hyper Transfer Markup Language",
                                        "High Text Modern Language"
                                    ],
                                    correctAnswer: 0
                                }
                            ],
                            createdAt: new Date().toISOString()
                        };
                        
                        if (!this.quizzes[userId]) {
                            this.quizzes[userId] = [];
                        }
                        
                        this.quizzes[userId].push(quiz);
                        localStorage.setItem('NoteSparkQuizzes', JSON.stringify(this.quizzes));
                        
                        resolve({ success: true, quiz });
                    }, 1500);
                });
            }
            
            async getQuizzes(userId) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(this.quizzes[userId] || []);
                    }, 500);
                });
            }
            
            // AI Chat
            async sendMessage(userId, message) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        // Simple AI response simulation
                        const responses = {
                            "hello": "Hello! How can I help you with your studies today?",
                            "hi": "Hi there! I'm your AI study assistant. What would you like to know?",
                            "explain binary search": "Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.",
                            "what is data structure": "A data structure is a particular way of organizing data in a computer so that it can be used effectively. Common data structures include arrays, linked lists, stacks, queues, trees, and graphs.",
                            "help": "I can help you with:\n- Explaining concepts\n- Generating study plans\n- Creating quizzes\n- Answering questions about your courses\n\nWhat would you like assistance with?",
                            "default": "I'm here to help with your studies! You can ask me to explain concepts, help with problem solving, or generate study materials. What specific topic are you working on?"
                        };
                        
                        const lowerMessage = message.toLowerCase();
                        let response = responses.default;
                        
                        for (const key in responses) {
                            if (lowerMessage.includes(key)) {
                                response = responses[key];
                                break;
                            }
                        }
                        
                        // Store chat history
                        if (!this.chats[userId]) {
                            this.chats[userId] = [];
                        }
                        
                        this.chats[userId].push({
                            user: message,
                            ai: response,
                            timestamp: new Date().toISOString()
                        });
                        
                        localStorage.setItem('NoteSparkChats', JSON.stringify(this.chats));
                        
                        resolve({ success: true, response });
                    }, 1000);
                });
            }
            
            async getChatHistory(userId) {
                return new Promise((resolve) => {
                    setTimeout(() => {
                        resolve(this.chats[userId] || []);
                    }, 300);
                });
            }
        }

        // Global variables
        const backendAPI = new BackendAPI();
        let currentUser = null;

        // Utility Functions
        function showNotification(message, type = 'info') {
            const notification = document.getElementById('notification');
            notification.textContent = message;
            notification.className = `notification ${type} show`;
            
            setTimeout(() => {
                notification.classList.remove('show');
            }, 3000);
        }

        function showLoading(buttonId) {
            const button = document.getElementById(buttonId);
            const spinner = document.getElementById(`${buttonId}-spinner`);
            const text = document.getElementById(`${buttonId}-text`);
            
            if (button && spinner && text) {
                button.disabled = true;
                text.style.display = 'none';
                spinner.classList.remove('hidden');
            }
        }

        function hideLoading(buttonId) {
            const button = document.getElementById(buttonId);
            const spinner = document.getElementById(`${buttonId}-spinner`);
            const text = document.getElementById(`${buttonId}-text`);
            
            if (button && spinner && text) {
                button.disabled = false;
                text.style.display = 'inline';
                spinner.classList.add('hidden');
            }
        }

        // Authentication and Page Management
        function showPage(pageId) {
            document.querySelectorAll('.page').forEach(page => {
                page.classList.remove('active');
            });
            document.getElementById(pageId).classList.add('active');
        }

        function checkAuthStatus() {
            const userData = JSON.parse(localStorage.getItem('NoteSparkCurrentUser'));
            
            if (userData) {
                currentUser = userData;
                showPage('dashboard-page');
                loadDashboardData();
            } else {
                showPage('signup-page');
            }
        }

        function loadDashboardData() {
            if (!currentUser) return;
            
            // Update user info
            document.getElementById('user-initial').textContent = currentUser.firstName.charAt(0);
            document.getElementById('user-initial-small').textContent = currentUser.firstName.charAt(0);
            
            // Load notes
            loadUserNotes();
            
            // Load quizzes count
            loadQuizzesCount();
            
            // Load AI chat history
            loadChatHistory();
        }

        async function loadUserNotes() {
            if (!currentUser) return;
            
            try {
                const notes = await backendAPI.getNotes(currentUser.id);
                const notesList = document.getElementById('notes-list');
                const notesCount = document.getElementById('notes-count');
                const notesCountSmall = document.getElementById('notes-count-small');
                
                // Update counts
                notesCount.textContent = notes.length;
                notesCountSmall.textContent = `${notes.length} files`;
                
                // Clear existing notes
                notesList.innerHTML = '';
                
                // Add notes to the list
                if (notes.length === 0) {
                    notesList.innerHTML = '<p class="text-gray-500 text-center py-4">No notes yet. Upload your first note!</p>';
                } else {
                    notes.forEach(note => {
                        const noteElement = document.createElement('div');
                        noteElement.className = 'flex items-center justify-between p-2 bg-gray-700 rounded-lg';
                        noteElement.innerHTML = `
                            <div class="flex items-center">
                                <div class="w-8 h-8 ${note.type === 'data-structures' ? 'bg-indigo-600' : 'bg-emerald-600'} rounded-lg flex items-center justify-center mr-3">
                                    <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                                    </svg>
                                </div>
                                <div>
                                    <div class="text-sm font-medium">${note.title}</div>
                                    <div class="text-xs text-gray-400">${formatDate(note.createdAt)}</div>
                                </div>
                            </div>
                            <button class="text-gray-400 hover:text-white delete-note" data-id="${note.id}">
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                                </svg>
                            </button>
                        `;
                        notesList.appendChild(noteElement);
                    });
                    
                    // Add event listeners to delete buttons
                    document.querySelectorAll('.delete-note').forEach(button => {
                        button.addEventListener('click', function() {
                            const noteId = this.getAttribute('data-id');
                            deleteNote(noteId);
                        });
                    });
                }
            } catch (error) {
                console.error('Error loading notes:', error);
                showNotification('Failed to load notes', 'error');
            }
        }

        async function loadQuizzesCount() {
            if (!currentUser) return;
            
            try {
                const quizzes = await backendAPI.getQuizzes(currentUser.id);
                document.getElementById('quizzes-count').textContent = quizzes.length;
            } catch (error) {
                console.error('Error loading quizzes count:', error);
            }
        }

        async function loadChatHistory() {
            if (!currentUser) return;
            
            try {
                const chatHistory = await backendAPI.getChatHistory(currentUser.id);
                const chatContainer = document.getElementById('ai-chat');
                
                // Clear existing chat
                chatContainer.innerHTML = '';
                
                // Add chat history
                chatHistory.forEach(chat => {
                    // User message
                    const userMessage = document.createElement('div');
                    userMessage.className = 'bg-indigo-600 rounded-lg p-4 ml-auto max-w-xs';
                    userMessage.innerHTML = `<p class="text-sm">${chat.user}</p>`;
                    chatContainer.appendChild(userMessage);
                    
                    // AI response
                    const aiMessage = document.createElement('div');
                    aiMessage.className = 'bg-gray-700 rounded-lg p-4 max-w-xs';
                    aiMessage.innerHTML = `<p class="text-sm">${chat.ai}</p>`;
                    chatContainer.appendChild(aiMessage);
                });
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
            } catch (error) {
                console.error('Error loading chat history:', error);
            }
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('en-US', { month: 'short', day: 'numeric', year: 'numeric' });
        }

        // Note Management
        async function uploadNote(file) {
            if (!currentUser) return;
            
            try {
                // Simulate file upload
                const noteData = {
                    title: file.name,
                    type: file.name.includes('data') ? 'data-structures' : 'algorithms',
                    fileSize: file.size,
                    fileType: file.type
                };
                
                await backendAPI.addNote(currentUser.id, noteData);
                showNotification('Note uploaded successfully', 'success');
                loadUserNotes();
            } catch (error) {
                console.error('Error uploading note:', error);
                showNotification('Failed to upload note', 'error');
            }
        }

        async function deleteNote(noteId) {
            if (!currentUser) return;
            
            try {
                await backendAPI.deleteNote(currentUser.id, noteId);
                showNotification('Note deleted successfully', 'success');
                loadUserNotes();
            } catch (error) {
                console.error('Error deleting note:', error);
                showNotification('Failed to delete note', 'error');
            }
        }

        // Quiz Generation
        async function generateQuiz(type, source) {
            if (!currentUser) return;
            
            try {
                showLoading('generate-quiz-btn');
                const result = await backendAPI.generateQuiz(currentUser.id, type, source);
                showNotification(`${type} quiz generated successfully!`, 'success');
                loadQuizzesCount();
            } catch (error) {
                console.error('Error generating quiz:', error);
                showNotification('Failed to generate quiz', 'error');
            } finally {
                hideLoading('generate-quiz-btn');
            }
        }

        // AI Chat
        async function sendChatMessage() {
            const input = document.getElementById('ai-chat-input');
            const message = input.value.trim();
            
            if (!message || !currentUser) return;
            
            // Add user message to chat
            const chatContainer = document.getElementById('ai-chat');
            const userMessage = document.createElement('div');
            userMessage.className = 'bg-indigo-600 rounded-lg p-4 ml-auto max-w-xs';
            userMessage.innerHTML = `<p class="text-sm">${message}</p>`;
            chatContainer.appendChild(userMessage);
            
            // Clear input
            input.value = '';
            
            // Scroll to bottom
            chatContainer.scrollTop = chatContainer.scrollHeight;
            
            // Get AI response
            try {
                const result = await backendAPI.sendMessage(currentUser.id, message);
                
                // Add AI response to chat
                const aiMessage = document.createElement('div');
                aiMessage.className = 'bg-gray-700 rounded-lg p-4 max-w-xs';
                aiMessage.innerHTML = `<p class="text-sm">${result.response}</p>`;
                chatContainer.appendChild(aiMessage);
                
                // Scroll to bottom again
                chatContainer.scrollTop = chatContainer.scrollHeight;
            } catch (error) {
                console.error('Error getting AI response:', error);
                
                // Show error message
                const errorMessage = document.createElement('div');
                errorMessage.className = 'bg-red-600 rounded-lg p-4 max-w-xs';
                errorMessage.innerHTML = `<p class="text-sm">Sorry, I'm having trouble responding right now. Please try again later.</p>`;
                chatContainer.appendChild(errorMessage);
                
                // Scroll to bottom
                chatContainer.scrollTop = chatContainer.scrollHeight;
            }
        }

        // File Upload Modal
        function showUploadModal() {
            document.getElementById('upload-modal').classList.remove('hidden');
        }

        function hideUploadModal() {
            document.getElementById('upload-modal').classList.add('hidden');
            document.getElementById('selected-files').classList.add('hidden');
            document.getElementById('file-list').innerHTML = '';
        }

        function handleFileSelect(files) {
            const fileList = document.getElementById('file-list');
            const selectedFiles = document.getElementById('selected-files');
            
            fileList.innerHTML = '';
            
            if (files.length > 0) {
                selectedFiles.classList.remove('hidden');
                
                for (let i = 0; i < files.length; i++) {
                    const file = files[i];
                    const fileItem = document.createElement('div');
                    fileItem.className = 'flex items-center justify-between bg-gray-700 p-2 rounded';
                    fileItem.innerHTML = `
                        <div class="flex items-center">
                            <svg class="w-4 h-4 text-gray-400 mr-2" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 12h6m-6 4h6m2 5H7a2 2 0 01-2-2V5a2 2 0 012-2h5.586a1 1 0 01.707.293l5.414 5.414a1 1 0 01.293.707V19a2 2 0 01-2 2z"></path>
                            </svg>
                            <span class="text-sm">${file.name}</span>
                        </div>
                        <span class="text-xs text-gray-400">${(file.size / 1024).toFixed(2)} KB</span>
                    `;
                    fileList.appendChild(fileItem);
                }
            } else {
                selectedFiles.classList.add('hidden');
            }
        }

        // Event Listeners
        document.addEventListener('DOMContentLoaded', function() {
            // Check authentication status
            checkAuthStatus();
            
            // Form Handling
            document.getElementById('signup-form').addEventListener('submit', async function(e) {
                e.preventDefault();
                
                const firstName = document.getElementById('first-name').value;
                const lastName = document.getElementById('last-name').value;
                const email = document.getElementById('email').value;
                const year = document.getElementById('year').value;
                const section = document.getElementById('section').value;
                const group = document.getElementById('group').value;
                const password = document.getElementById('password').value;
                
                if (!firstName || !lastName || !email || !year || !section || !group || !password) {
                    showNotification('Please fill all fields', 'error');
                    return;
                }
                
                try {
                    showLoading('signup');
                    const result = await backendAPI.signup({
                        firstName,
                        lastName,
                        email,
                        year,
                        section,
                        group,
                        password
                    });
                    
                    if (result.success) {
                        currentUser = result.user;
                        localStorage.setItem('NoteSparkCurrentUser', JSON.stringify(currentUser));
                        showNotification('Account created successfully!', 'success');
                        showPage('dashboard-page');
                        loadDashboardData();
                    }
                } catch (error) {
                    showNotification(error.message || 'Signup failed', 'error');
                } finally {
                    hideLoading('signup');
                }
            });

            document.getElementById('login-form').addEventListener('submit', async function(e) {
                e.preventDefault();
                
                const email = document.getElementById('login-email').value;
                const password = document.getElementById('login-password').value;
                
                if (!email || !password) {
                    showNotification('Please fill all fields', 'error');
                    return;
                }
                
                try {
                    showLoading('login');
                    const result = await backendAPI.login(email, password);
                    
                    if (result.success) {
                        currentUser = result.user;
                        localStorage.setItem('NoteSparkCurrentUser', JSON.stringify(currentUser));
                        showNotification('Login successful!', 'success');
                        showPage('dashboard-page');
                        loadDashboardData();
                    }
                } catch (error) {
                    showNotification(error.message || 'Login failed', 'error');
                } finally {
                    hideLoading('login');
                }
            });

            document.getElementById('logout-btn').addEventListener('click', function() {
                localStorage.removeItem('NoteSparkCurrentUser');
                currentUser = null;
                showPage('login-page');
                showNotification('Logged out successfully', 'info');
            });

            document.getElementById('show-login').addEventListener('click', function(e) {
                e.preventDefault();
                showPage('login-page');
            });

            document.getElementById('show-signup').addEventListener('click', function(e) {
                e.preventDefault();
                showPage('signup-page');
            });

            // Dashboard Actions
            document.getElementById('upload-notes-btn').addEventListener('click', showUploadModal);
            document.getElementById('upload-new-notes').addEventListener('click', showUploadModal);
            
            document.getElementById('generate-quiz-btn').addEventListener('click', function() {
                generateQuiz('General', 'AI');
            });
            
            document.getElementById('generate-from-notes').addEventListener('click', function() {
                generateQuiz('Notes', 'Your Notes');
            });
            
            document.getElementById('generate-from-pyqs').addEventListener('click', function() {
                generateQuiz('PYQ', 'Previous Year Questions');
            });

            // AI Chat
            document.getElementById('ai-chat-send').addEventListener('click', sendChatMessage);
            
            document.getElementById('ai-chat-input').addEventListener('keypress', function(e) {
                if (e.key === 'Enter') {
                    sendChatMessage();
                }
            });

            // File Upload Modal
            document.getElementById('file-input').addEventListener('change', function(e) {
                handleFileSelect(e.target.files);
            });

            document.getElementById('close-upload-modal').addEventListener('click', hideUploadModal);
            document.getElementById('cancel-upload').addEventListener('click', hideUploadModal);
            
            document.getElementById('confirm-upload').addEventListener('click', function() {
                const files = document.getElementById('file-input').files;
                
                if (files.length === 0) {
                    showNotification('Please select at least one file', 'error');
                    return;
                }
                
                // Simulate file upload for each file
                for (let i = 0; i < files.length; i++) {
                    uploadNote(files[i]);
                }
                
                hideUploadModal();
            });

            // Support Section Actions
            document.getElementById('ai-help-chat').addEventListener('click', function() {
                document.getElementById('ai-chat-input').focus();
                document.getElementById('ai-tools').scrollIntoView({ behavior: 'smooth' });
            });

            document.getElementById('video-tutorials').addEventListener('click', function() {
                showNotification('Video tutorials feature coming soon!', 'info');
            });

            document.getElementById('suggestions-btn').addEventListener('click', function() {
                showNotification('Thank you for your interest! Please email your suggestions to aryanshukla1918@gmail.com', 'info');
            });

            // Smooth scrolling for anchor links
            document.querySelectorAll('a[href^="#"]').forEach(anchor => {
                anchor.addEventListener('click', function (e) {
                    e.preventDefault();
                    
                    const targetId = this.getAttribute('href');
                    if (targetId === '#') return;
                    
                    const targetElement = document.querySelector(targetId);
                    if (targetElement) {
                        window.scrollTo({
                            top: targetElement.offsetTop - 100,
                            behavior: 'smooth'
                        });
                    }
                });
            });
        });

        // Three.js Background Animation
        function initThreeJS() {
            const scene = new THREE.Scene();
            const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
            const renderer = new THREE.WebGLRenderer({ alpha: true });
            renderer.setSize(window.innerWidth, window.innerHeight);
            document.getElementById('threejs-background').appendChild(renderer.domElement);
            
            // Create floating geometric shapes
            const geometry = new THREE.IcosahedronGeometry(1, 0);
            const material = new THREE.MeshBasicMaterial({ 
                color: 0x6366F1, 
                wireframe: true,
                transparent: true,
                opacity: 0.1
            });
            
            const shapes = [];
            for (let i = 0; i < 10; i++) {
                const shape = new THREE.Mesh(geometry, material);
                shape.position.x = Math.random() * 40 - 20;
                shape.position.y = Math.random() * 40 - 20;
                shape.position.z = Math.random() * 40 - 20;
                shape.rotation.x = Math.random() * Math.PI;
                shape.rotation.y = Math.random() * Math.PI;
                shapes.push(shape);
                scene.add(shape);
            }
            
            camera.position.z = 30;
            
            // Animation
            function animate() {
                requestAnimationFrame(animate);
                
                shapes.forEach(shape => {
                    shape.rotation.x += 0.005;
                    shape.rotation.y += 0.005;
                });
                
                renderer.render(scene, camera);
            }
            
            animate();
            
            // Handle window resize
            window.addEventListener('resize', () => {
                camera.aspect = window.innerWidth / window.innerHeight;
                camera.updateProjectionMatrix();
                renderer.setSize(window.innerWidth, window.innerHeight);
            });
        }

        // Shooting Stars Animation
        function createShootingStar() {
            const star = document.createElement('div');
            star.className = 'shooting-star';
            
            // Random start position
            const startX = Math.random() * window.innerWidth;
            const startY = Math.random() * window.innerHeight / 2;
            
            // Random trajectory
            const endX = startX + 200 + Math.random() * 300;
            const endY = startY + 100 + Math.random() * 200;
            
            // Apply styles
            star.style.left = startX + 'px';
            star.style.top = startY + 'px';
            
            // Animation
            star.animate([
                { transform: `translate(0, 0)`, opacity: 0 },
                { transform: `translate(0, 0)`, opacity: 1 },
                { transform: `translate(${endX - startX}px, ${endY - startY}px)`, opacity: 0 }
            ], {
                duration: 2000 + Math.random() * 3000,
                easing: 'cubic-bezier(0.4, 0, 0.2, 1)'
            });
            
            document.querySelector('.space-bg').appendChild(star);
            
            // Remove element after animation
            setTimeout(() => {
                if (star.parentNode) {
                    star.parentNode.removeChild(star);
                }
            }, 5000);
        }

        // Create shooting stars periodically
        setInterval(createShootingStar, 2000);
        
        // Initial shooting stars
        for (let i = 0; i < 3; i++) {
            setTimeout(createShootingStar, i * 800);
        }

        // Initialize Three.js if available
        if (typeof THREE !== 'undefined') {
            initThreeJS();
        }
    </script>
</body>
</html>
