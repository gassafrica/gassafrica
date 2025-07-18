<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Samuel - Laravel Developer</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Consolas', 'Monaco', 'Courier New', monospace;
            background: #1e1e1e;
            color: #d4d4d4;
            overflow-x: hidden;
        }

        .vscode-container {
            min-height: 100vh;
            background: #1e1e1e;
            display: flex;
            flex-direction: column;
        }

        /* Title Bar */
        .title-bar {
            background: #323233;
            height: 35px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            border-bottom: 1px solid #2d2d30;
        }

        .window-controls {
            display: flex;
            gap: 8px;
            margin-left: auto;
        }

        .control-btn {
            width: 12px;
            height: 12px;
            border-radius: 50%;
            cursor: pointer;
            transition: opacity 0.2s;
        }

        .control-btn.close { background: #ff5f56; }
        .control-btn.minimize { background: #ffbd2e; }
        .control-btn.maximize { background: #27ca3f; }

        .control-btn:hover {
            opacity: 0.8;
        }

        .window-title {
            font-size: 12px;
            color: #cccccc;
            position: absolute;
            left: 50%;
            transform: translateX(-50%);
        }

        /* Menu Bar */
        .menu-bar {
            background: #2d2d30;
            height: 30px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            border-bottom: 1px solid #3e3e42;
        }

        .menu-item {
            padding: 5px 10px;
            font-size: 12px;
            color: #cccccc;
            cursor: pointer;
            transition: background 0.2s;
        }

        .menu-item:hover {
            background: #3e3e42;
        }

        /* Main Content */
        .main-content {
            flex: 1;
            display: flex;
            background: #1e1e1e;
        }

        /* Sidebar */
        .sidebar {
            width: 250px;
            background: #252526;
            border-right: 1px solid #2d2d30;
            display: flex;
            flex-direction: column;
            transition: width 0.3s ease;
        }

        .sidebar-header {
            padding: 10px;
            border-bottom: 1px solid #2d2d30;
            font-size: 11px;
            color: #cccccc;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        .file-explorer {
            flex: 1;
            padding: 10px 0;
        }

        .file-item {
            padding: 8px 20px;
            display: flex;
            align-items: center;
            color: #cccccc;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 13px;
        }

        .file-item:hover {
            background: #2a2d2e;
        }

        .file-item.active {
            background: #37373d;
            color: #ffffff;
        }

        .file-icon {
            margin-right: 8px;
            font-size: 14px;
        }

        .folder-icon {
            color: #dcb67a;
        }

        .php-icon {
            color: #ff6b6b;
        }

        .js-icon {
            color: #f7df1e;
        }

        .css-icon {
            color: #42a5f5;
        }

        /* Editor Area */
        .editor-area {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .tab-bar {
            background: #2d2d30;
            height: 35px;
            display: flex;
            align-items: center;
            border-bottom: 1px solid #3e3e42;
            overflow-x: auto;
        }

        .tab {
            padding: 0 15px;
            height: 100%;
            display: flex;
            align-items: center;
            background: #2d2d30;
            color: #969696;
            cursor: pointer;
            border-right: 1px solid #3e3e42;
            transition: all 0.2s;
            font-size: 12px;
            white-space: nowrap;
            position: relative;
        }

        .tab.active {
            background: #1e1e1e;
            color: #ffffff;
        }

        .tab::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            height: 2px;
            background: #ff2d20;
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .tab.active::after {
            transform: scaleX(1);
        }

        .tab-icon {
            margin-right: 6px;
        }

        .tab-close {
            margin-left: 6px;
            opacity: 0;
            transition: opacity 0.2s;
        }

        .tab:hover .tab-close {
            opacity: 1;
        }

        /* Editor Content */
        .editor-content {
            flex: 1;
            background: #1e1e1e;
            padding: 20px;
            overflow-y: auto;
            position: relative;
        }

        .line-numbers {
            position: absolute;
            left: 0;
            top: 20px;
            width: 50px;
            background: #1e1e1e;
            color: #858585;
            font-size: 12px;
            line-height: 1.6;
            padding: 0 10px;
            text-align: right;
            user-select: none;
        }

        .code-content {
            margin-left: 60px;
            line-height: 1.6;
            font-size: 14px;
        }

        /* Syntax Highlighting */
        .keyword { color: #569cd6; }
        .string { color: #ce9178; }
        .comment { color: #6a9955; font-style: italic; }
        .function { color: #dcdcaa; }
        .variable { color: #9cdcfe; }
        .tag { color: #ff6b6b; }
        .attribute { color: #92c5f7; }
        .laravel { color: #ff2d20; font-weight: bold; }

        /* Animations */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }

        @keyframes slideIn {
            from { transform: translateX(-100%); }
            to { transform: translateX(0); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.05); }
        }

        .animate-fade-in {
            animation: fadeIn 0.6s ease-out;
        }

        .animate-slide-in {
            animation: slideIn 0.5s ease-out;
        }

        .pulse-animation {
            animation: pulse 2s infinite;
        }

        /* Status Bar */
        .status-bar {
            background: #007acc;
            height: 22px;
            display: flex;
            align-items: center;
            padding: 0 10px;
            font-size: 11px;
            color: #ffffff;
        }

        .status-item {
            margin-right: 20px;
            cursor: pointer;
            transition: opacity 0.2s;
        }

        .status-item:hover {
            opacity: 0.8;
        }

        .laravel-logo {
            color: #ff2d20;
            font-weight: bold;
            margin-right: 5px;
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .sidebar {
                width: 200px;
            }
            
            .main-content {
                flex-direction: column;
            }
            
            .sidebar {
                width: 100%;
                height: auto;
                order: 2;
            }
            
            .editor-area {
                order: 1;
            }
            
            .code-content {
                margin-left: 40px;
                font-size: 12px;
            }
            
            .line-numbers {
                width: 35px;
                font-size: 10px;
            }
        }

        @media (max-width: 480px) {
            .sidebar {
                display: none;
            }
            
            .code-content {
                margin-left: 20px;
                font-size: 11px;
            }
            
            .line-numbers {
                display: none;
            }
            
            .editor-content {
                padding: 10px;
            }
        }

        /* Hover Effects */
        .hover-effect:hover {
            transform: translateY(-2px);
            transition: transform 0.2s ease;
        }

        /* Glowing Effect */
        .glow {
            box-shadow: 0 0 20px rgba(255, 45, 32, 0.3);
        }

        /* Typing Animation */
        .typing-animation {
            border-right: 2px solid #ff2d20;
            animation: blink 1s infinite;
        }

        @keyframes blink {
            0%, 50% { border-color: #ff2d20; }
            51%, 100% { border-color: transparent; }
        }

        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }

        ::-webkit-scrollbar-track {
            background: #2d2d30;
        }

        ::-webkit-scrollbar-thumb {
            background: #424242;
            border-radius: 4px;
        }

        ::-webkit-scrollbar-thumb:hover {
            background: #4f4f4f;
        }
    </style>
</head>
<body>
    <div class="vscode-container">
        <!-- Title Bar -->
        <div class="title-bar">
            <div class="window-title">Samuel - Laravel Developer</div>
            <div class="window-controls">
                <div class="control-btn close"></div>
                <div class="control-btn minimize"></div>
                <div class="control-btn maximize"></div>
            </div>
        </div>

        <!-- Menu Bar -->
        <div class="menu-bar">
            <div class="menu-item">File</div>
            <div class="menu-item">Edit</div>
            <div class="menu-item">View</div>
            <div class="menu-item">Terminal</div>
            <div class="menu-item">Help</div>
        </div>

        <!-- Main Content -->
        <div class="main-content">
            <!-- Sidebar -->
            <div class="sidebar animate-slide-in">
                <div class="sidebar-header">
                    <span class="laravel-logo">⚡</span> Samuel's Portfolio
                </div>
                <div class="file-explorer">
                    <div class="file-item active hover-effect" onclick="switchTab('about')">
                        <span class="file-icon php-icon">🍄</span>
                        <span>About.php</span>
                    </div>
                    <div class="file-item hover-effect" onclick="switchTab('skills')">
                        <span class="file-icon js-icon">⚡</span>
                        <span>Skills.js</span>
                    </div>
                    <div class="file-item hover-effect" onclick="switchTab('projects')">
                        <span class="file-icon css-icon">🚀</span>
                        <span>Projects.css</span>
                    </div>
                    <div class="file-item hover-effect" onclick="switchTab('contact')">
                        <span class="file-icon folder-icon">📧</span>
                        <span>Contact.json</span>
                    </div>
                </div>
            </div>

            <!-- Editor Area -->
            <div class="editor-area">
                <!-- Tab Bar -->
                <div class="tab-bar">
                    <div class="tab active" id="tab-about">
                        <span class="tab-icon php-icon">🍄</span>
                        <span>About.php</span>
                        <span class="tab-close">×</span>
                    </div>
                    <div class="tab" id="tab-skills">
                        <span class="tab-icon js-icon">⚡</span>
                        <span>Skills.js</span>
                        <span class="tab-close">×</span>
                    </div>
                    <div class="tab" id="tab-projects">
                        <span class="tab-icon css-icon">🚀</span>
                        <span>Projects.css</span>
                        <span class="tab-close">×</span>
                    </div>
                    <div class="tab" id="tab-contact">
                        <span class="tab-icon folder-icon">📧</span>
                        <span>Contact.json</span>
                        <span class="tab-close">×</span>
                    </div>
                </div>

                <!-- Editor Content -->
                <div class="editor-content">
                    <div class="line-numbers" id="line-numbers">
                        1<br>2<br>3<br>4<br>5<br>6<br>7<br>8<br>9<br>10<br>11<br>12<br>13<br>14<br>15<br>16<br>17<br>18<br>19<br>20<br>21<br>22<br>23<br>24<br>25<br>26<br>27<br>28<br>29<br>30
                    </div>
                    
                    <div class="code-content animate-fade-in" id="content-about">
<span class="comment">// Samuel - Full Stack Laravel Developer from Ghana 🇬🇭</span>
<span class="keyword">&lt;?php</span>

<span class="keyword">namespace</span> <span class="laravel">App\Developer</span>;

<span class="keyword">use</span> <span class="laravel">Illuminate\Support\Facades\Artisan</span>;
<span class="keyword">use</span> <span class="laravel">Illuminate\Foundation\Auth\User</span>;

<span class="keyword">class</span> <span class="function">Samuel</span> <span class="keyword">extends</span> <span class="laravel">User</span>
{
    <span class="keyword">protected</span> <span class="variable">$fillable</span> = [
        <span class="string">'name'</span> => <span class="string">'Samuel'</span>,
        <span class="string">'location'</span> => <span class="string">'Ghana 🇬🇭'</span>,
        <span class="string">'role'</span> => <span class="string">'Full Stack Developer'</span>,
        <span class="string">'passion'</span> => <span class="string">'Laravel & Python'</span>,
        <span class="string">'hobbies'</span> => [<span class="string">'🎵 Music'</span>, <span class="string">'⚽ FIFA'</span>, <span class="string">'🎮 Gaming'</span>],
        <span class="string">'motto'</span> => <span class="string">'Code + Music + FIFA = Pure Magic!'</span>
    ];

    <span class="keyword">public function</span> <span class="function">createMagic</span>()
    {
        <span class="keyword">return</span> <span class="laravel">Artisan</span>::<span class="function">call</span>(<span class="string">'make:legendary-solution'</span>);
    }

    <span class="keyword">public function</span> <span class="function">getSpecialAbilities</span>()
    {
        <span class="keyword">return</span> [
            <span class="string">'🎵 Coding with perfect soundtrack'</span>,
            <span class="string">'⚽ FIFA champion reflexes'</span>,
            <span class="string">'🚀 Problem-solving wizard'</span>,
            <span class="string">'💻 Laravel & Python mastery'</span>
        ];
    }
}
                    </div>

                    <div class="code-content" id="content-skills" style="display: none;">
<span class="comment">// My Technical Arsenal 🛠️</span>
<span class="keyword">const</span> <span class="variable">skills</span> = {
    <span class="attribute">backend</span>: {
        <span class="laravel">php</span>: <span class="string">'🍄 Expert Level - Laravel Master'</span>,
        <span class="laravel">laravel</span>: <span class="string">'⚡ Advanced - Framework Wizard'</span>,
        <span class="variable">python</span>: <span class="string">'🐍 Advanced - Django & Flask'</span>,
        <span class="variable">databases</span>: [<span class="string">'MySQL'</span>, <span class="string">'SQLite'</span>]
    },
    
    <span class="attribute">frontend</span>: {
        <span class="variable">javascript</span>: <span class="string">'💚 Vue.js Specialist'</span>,
        <span class="variable">mobile</span>: <span class="string">'📱 Ionic Framework'</span>,
        <span class="variable">css</span>: <span class="string">'🎨 Modern Responsive Design'</span>
    },
    
    <span class="attribute">tools</span>: {
        <span class="variable">git</span>: <span class="string">'⚡ Version Control Master'</span>,
        <span class="variable">cpanel</span>: <span class="string">'🎮 Server Management'</span>,
        <span class="variable">deployment</span>: <span class="string">'🚀 Production Ready'</span>
    },
    
    <span class="attribute">superpowers</span>: [
        <span class="string">'🎵 Coding with perfect music timing'</span>,
        <span class="string">'⚽ FIFA-level precision in debugging'</span>,
        <span class="string">'🎮 Gaming-inspired problem solving'</span>,
        <span class="string">'💡 Innovation through creativity'</span>
    ]
};

<span class="comment">// Ready to build something amazing? 🚀</span>
<span class="keyword">console</span>.<span class="function">log</span>(<span class="string">'Let\\'s create digital magic together!'</span>);
                    </div>

                    <div class="code-content" id="content-projects" style="display: none;">
<span class="comment">/* Portfolio Showcase - Built with Laravel & Love */</span>
<span class="keyword">@import</span> <span class="string">'passion.css'</span>;
<span class="keyword">@import</span> <span class="string">'innovation.css'</span>;

<span class="tag">.portfolio-projects</span> {
    <span class="attribute">display</span>: <span class="string">legendary</span>;
    <span class="attribute">framework</span>: <span class="laravel">Laravel</span>;
    <span class="attribute">language</span>: <span class="string">PHP & Python</span>;
    <span class="attribute">mobile</span>: <span class="string">Ionic Ready</span>;
    <span class="attribute">passion</span>: <span class="string">infinite</span>;
}

<span class="tag">.web-applications</span> {
    <span class="attribute">type</span>: <span class="string">'Full Stack Solutions'</span>;
    <span class="attribute">features</span>: [
        <span class="string">'🚀 Laravel Backend APIs'</span>,
        <span class="string">'💚 Vue.js Frontend'</span>,
        <span class="string">'📱 Mobile-First Design'</span>,
        <span class="string">'🔐 Authentication Systems'</span>
    ];
}

<span class="tag">.mobile-apps</span> {
    <span class="attribute">platform</span>: <span class="string">'Cross-Platform'</span>;
    <span class="attribute">technology</span>: <span class="string">'Ionic Framework'</span>;
    <span class="attribute">performance</span>: <span class="string">'FIFA-level smooth'</span>;
}

<span class="tag">.specializations</span> {
    <span class="attribute">e-commerce</span>: <span class="string">'🛒 Complete Solutions'</span>;
    <span class="attribute">cms</span>: <span class="string">'📝 Custom Content Management'</span>;
    <span class="attribute">apis</span>: <span class="string">'🔗 RESTful & GraphQL'</span>;
    <span class="attribute">integrations</span>: <span class="string">'🌐 Third-party Services'</span>;
}

<span class="comment">/* Every project is crafted with music, passion, and FIFA breaks! */</span>
<span class="tag">.development-process</span> {
    <span class="attribute">methodology</span>: <span class="string">'Agile with a touch of magic'</span>;
    <span class="attribute">testing</span>: <span class="string">'PHPUnit & Jest'</span>;
    <span class="attribute">deployment</span>: <span class="string">'CI/CD Pipeline'</span>;
    <span class="attribute">maintenance</span>: <span class="string">'24/7 Support'</span>;
}
                    </div>

                    <div class="code-content" id="content-contact" style="display: none;">
<span class="comment">// Let's Connect and Build Something Amazing! 🚀</span>
{
    <span class="attribute">"developer"</span>: {
        <span class="attribute">"name"</span>: <span class="string">"Samuel"</span>,
        <span class="attribute">"title"</span>: <span class="string">"Full Stack Laravel Developer"</span>,
        <span class="attribute">"location"</span>: <span class="string">"Ghana 🇬🇭"</span>,
        <span class="attribute">"availability"</span>: <span class="string">"Ready for epic collaborations!"</span>
    },
    
    <span class="attribute">"contact_channels"</span>: {
        <span class="attribute">"email"</span>: <span class="string">"gassdj47@gmail.com"</span>,
        <span class="attribute">"instagram"</span>: <span class="string">"@akwesigyekye01"</span>,
        <span class="attribute">"youtube"</span>: <span class="string">"@gassbuilds"</span>,
        <span class="attribute">"twitter"</span>: <span class="string">"@sarpongakwesi"</span>,
        <span class="attribute">"github"</span>: <span class="string">"@gassafrica"</span>
    },
    
    <span class="attribute">"services"</span>: [
        <span class="string">"🌐 Web Application Development"</span>,
        <span class="string">"📱 Mobile App Development"</span>,
        <span class="string">"🛒 E-commerce Solutions"</span>,
        <span class="string">"🔗 API Development & Integration"</span>,
        <span class="string">"💻 Custom Laravel Solutions"</span>,
        <span class="string">"🚀 Performance Optimization"</span>
    ],
    
    <span class="attribute">"collaboration_style"</span>: {
        <span class="attribute">"communication"</span>: <span class="string">"Clear and responsive"</span>,
        <span class="attribute">"project_management"</span>: <span class="string">"Agile methodology"</span>,
        <span class="attribute">"code_quality"</span>: <span class="string">"Clean, tested, documented"</span>,
        <span class="attribute">"timeline"</span>: <span class="string">"Reliable delivery"</span>
    },
    
    <span class="attribute">"fun_fact"</span>: <span class="string">"I code better with music and FIFA breaks! 🎵⚽"</span>,
    
    <span class="attribute">"call_to_action"</span>: <span class="string">"Ready to turn your ideas into digital reality? Let's chat!"</span>
}
                    </div>
                </div>
            </div>
        </div>

        <!-- Status Bar -->
        <div class="status-bar">
            <div class="status-item">
                <span class="laravel-logo">⚡</span>
                <span>Laravel</span>
            </div>
            <div class="status-item">UTF-8</div>
            <div class="status-item">PHP</div>
            <div class="status-item">Ln 1, Col 1</div>
            <div class="status-item">Ghana 🇬🇭</div>
            <div class="status-item pulse-animation">🎵 Coding Mode</div>
        </div>
    </div>

    <script>
        // Tab switching functionality
        function switchTab(tabName) {
            // Hide all content
            document.querySelectorAll('.code-content').forEach(content => {
                content.style.display = 'none';
            });
            
            // Remove active class from all tabs
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Remove active class from all file items
            document.querySelectorAll('.file-item').forEach(item => {
                item.classList.remove('active');
            });
            
            // Show selected content
            document.getElementById('content-' + tabName).style.display = 'block';
            
            // Add active class to selected tab
            document.getElementById('tab-' + tabName).classList.add('active');
            
            // Add active class to selected file item
            event.target.closest('.file-item').classList.add('active');
            
            // Add fade-in animation
            document.getElementById('content-' + tabName).classList.add('animate-fade-in');
        }

        // Add click events to tabs
        document.querySelectorAll('.tab').forEach(tab => {
            tab.addEventListener('click', function() {
                const tabName = this.id.replace('tab-', '');
                switchTab(tabName);
            });
        });

        // Typing animation effect
        let typingText = "Let's build something legendary together! 🚀";
        let typingElement = document.createElement('div');
        typingElement.className = 'typing-animation';
        typingElement.style.position = 'fixed';
        typingElement.style.bottom = '30px';
        typingElement.style.right = '20px';
        typingElement.style.color = '#ff2d20';
        typingElement.style.fontSize = '12px';
        typingElement.style.fontWeight = 'bold';
        typingElement.style.zIndex = '1000';
        document.body.appendChild(typingElement);

        let i = 0;
        function typeWriter() {
            if (i < typingText.length) {
                typingElement.textContent += typingText.charAt(i);
                i++;
                setTimeout(typeWriter, 100);
            } else {
                setTimeout(() => {
                    typingElement.textContent = '';
                    i = 0;
                    setTimeout(typeWriter, 2000);
                }, 3000);
            }
        }

        // Start typing animation after page load
        setTimeout(typeWriter, 2000);

        // Add hover effects to menu items
        document.querySelectorAll('.menu-item').forEach(item => {
            item.addEventListener('mouseenter', function() {
                this.style.backgroundColor = '#3e3e42';
            });
            item.addEventListener('mouseleave', function() {
                this.style.backgroundColor = 'transparent';
            });
        });

        // Add glow effect to Laravel elements
        document.querySelectorAll('.laravel').forEach(element => {
            element.addEventListener('mouseenter', function() {
                this.classList.add('glow');
            });
            element.addEventListener('mouseleave', function() {
                this.classList.remove('glow');
            });
        });

        // Responsive sidebar toggle
        function toggleSidebar() {
            const sidebar = document.querySelector('.sidebar');
            const currentWidth = window.getComputedStyle(sidebar).width;
            
            if (window.innerWidth <= 768) {
                sidebar.style.display = sidebar.style.display === 'none' ? 'flex' : 'none';
            }
        }

        // Add click event to window controls
        document.querySelectorAll('.control-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                this.style.transform = 'scale(0.9)';
                setTimeout(() => {
                    this.style.transform = 'scale(1)';
                }, 100);
            });
        });

        // Update line numbers based on content height
        function updateLineNumbers() {
            const activeContent = document.querySelector('.code-content:not([style*="display: none"])');
            if (activeContent) {
                const lines = activeContent.textContent.split('\n').length;
                const lineNumbers = document.getElementById('line-numbers');
                let numbersHTML = '';
                for (let i = 1; i <= Math.max(lines, 30); i++) {
                    numbersHTML += i + '<br>';
                }
                lineNumbers.innerHTML = numbersHTML;
            }
        }

        // Update line numbers on content change
        document.addEventListener('DOMContentLoaded', updateLineNumbers);
        
        // Add some interactive elements
        document.querySelectorAll('.hover-effect').forEach(element => {
            element.addEventListener('mouseenter', function() {
                this.style.transform = 'translateY(-2px)';
                this.style.boxShadow
