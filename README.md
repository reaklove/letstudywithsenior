# letstudywithsenior
<!DOCTYPE html>
<html lang="en" class="h-full">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Let study with senior Interactive Lesson Platform</title>
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Lucide Icons CDN -->
    <script src="https://unpkg.com/lucide@latest"></script>
    <!-- Inter Font -->
    <link href="https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <!-- PDF.js for parsing PDF files -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.min.js"></script>
    <!-- Mammoth.js for parsing Word docx files -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.6.0/mammoth.browser.min.js"></script>
    
    <script>
        // Configure PDF.js worker
        if (window.pdfjsLib) {
            window.pdfjsLib.GlobalWorkerOptions.workerSrc = 'https://cdnjs.cloudflare.com/ajax/libs/pdf.js/3.11.174/pdf.worker.min.js';
        }
    </script>
    <style>
        body { font-family: 'Plus Jakarta Sans', sans-serif; }
        ::-webkit-scrollbar { width: 6px; height: 6px; }
        ::-webkit-scrollbar-track { background: #f8fafc; }
        ::-webkit-scrollbar-thumb { background: #cbd5e1; border-radius: 9999px; }
        ::-webkit-scrollbar-thumb:hover { background: #94a3b8; }
        .glass-header {
            background: rgba(255, 255, 255, 0.85);
            backdrop-filter: blur(12px);
            -webkit-backdrop-filter: blur(12px);
        }
    </style>
</head>
<body class="bg-slate-900 text-slate-100 h-full flex flex-col antialiased selection:bg-indigo-500 selection:text-white">

    <header class="glass-header border-b border-slate-800/80 sticky top-0 z-40 transition-all">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-20 flex items-center justify-between">
            <div class="flex items-center space-x-3.5 cursor-pointer group" onclick="app.goHome()">
                <!-- Professional Logo Mark -->
                <div class="w-12 h-12 rounded-2xl bg-gradient-to-tr from-indigo-600 via-violet-600 to-pink-500 p-0.5 shadow-lg shadow-indigo-500/25 group-hover:scale-105 transition-transform duration-300">
                    <div class="w-full h-full bg-slate-900 rounded-[14px] flex items-center justify-center">
                        <i data-lucide="graduation-cap" class="w-6 h-6 text-indigo-400 group-hover:text-white transition-colors"></i>
                    </div>
                </div>
                <div>
                    <div class="flex items-center space-x-2">
                        <span class="font-extrabold text-xl tracking-tight bg-gradient-to-r from-white via-slate-100 to-slate-400 bg-clip-text text-transparent">LessonHub</span>
                        <span class="px-2 py-0.5 bg-indigo-500/25 text-indigo-300 border border-indigo-500/30 text-[10px] font-bold rounded-full uppercase tracking-wider">PRO</span>
                    </div>
                    <p class="text-xs text-slate-400 font-medium hidden sm:block">Advanced Enterprise Lesson Platform</p>
                </div>
            </div>
            
            <div class="flex items-center space-x-4">
                <div class="hidden md:flex items-center space-x-1 text-xs text-slate-400 bg-slate-800/60 border border-slate-700/60 px-3.5 py-2 rounded-xl">
                    <i data-lucide="sparkles" class="w-4 h-4 text-indigo-400"></i>
                    <span>Supports PDF, Word, MP4 & JSON Imports</span>
                </div>
                <button onclick="app.openModal()" class="inline-flex items-center space-x-2 bg-gradient-to-r from-indigo-600 to-violet-600 hover:from-indigo-500 hover:to-violet-500 text-white px-5 py-2.5 rounded-xl font-semibold text-sm shadow-xl shadow-indigo-600/30 transition-all transform hover:-translate-y-0.5 active:translate-y-0 cursor-pointer">
                    <i data-lucide="plus" class="w-4 h-4 stroke-[2.5]"></i>
                    <span>Create Lesson</span>
                </button>
            </div>
        </div>
    </header>

    <main class="flex-1 max-w-7xl w-full mx-auto px-4 sm:px-6 lg:px-8 py-8 flex flex-col overflow-hidden">
        
        <!-- View 1: Dashboard / Home -->
        <div id="home-view" class="flex-1 flex flex-col overflow-hidden">
            <!-- Hero Banner -->
            <div class="mb-8 bg-gradient-to-r from-indigo-950/60 via-slate-900 to-violet-950/40 border border-indigo-500/20 rounded-3xl p-6 sm:p-8 relative overflow-hidden shadow-2xl">
                <div class="absolute -right-10 -bottom-10 w-64 h-64 bg-indigo-500/10 rounded-full blur-3xl pointer-events-none"></div>
                <div class="relative z-10 max-w-2xl">
                    <span class="inline-flex items-center space-x-1.5 px-3 py-1 rounded-full bg-indigo-500/20 text-indigo-300 text-xs font-semibold mb-3 border border-indigo-500/30">
                        <i data-lucide="zap" class="w-3.5 h-3.5"></i>
                        <span>Interactive Learning Ecosystem</span>
                    </span>
                    <h2 class="text-2xl sm:text-4xl font-extrabold text-white tracking-tight mb-3">Empower minds with structured knowledge.</h2>
                    <p class="text-slate-300 text-sm sm:text-base leading-relaxed">Create, import, and read professional lessons seamlessly. Upload PDFs, Word documents, videos, or build custom step-by-step guides instantly.</p>
                </div>
            </div>

            <!-- Search and Filter Bar -->
            <div class="flex flex-col md:flex-row gap-4 mb-6 justify-between items-stretch md:items-center">
                <div class="relative flex-1 max-w-md">
                    <i data-lucide="search" class="absolute left-4 top-1/2 -translate-y-1/2 w-4 h-4 text-slate-400"></i>
                    <input type="text" id="search-input" oninput="app.handleSearch(event)" placeholder="Search by title, category, or content..." class="w-full pl-11 pr-4 py-3 bg-slate-800/80 border border-slate-700/80 rounded-2xl text-sm text-slate-100 placeholder-slate-400 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:border-transparent shadow-inner">
                </div>
                <div class="flex items-center space-x-2 overflow-x-auto pb-2 md:pb-0 scrollbar-none" id="category-filters">
                    <button onclick="app.filterCategory('All')" class="category-btn px-4 py-2.5 rounded-xl text-xs font-semibold bg-indigo-600 text-white whitespace-nowrap shadow-md transition-all cursor-pointer">All Categories</button>
                </div>
            </div>

            <!-- Lessons Grid Container -->
            <div class="flex-1 overflow-y-auto pr-1 pb-12">
                <div id="lessons-grid" class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                    <!-- Lessons rendered dynamically -->
                </div>
                <!-- Empty State -->
                <div id="empty-state" class="hidden flex flex-col items-center justify-center py-20 text-center">
                    <div class="w-20 h-20 bg-slate-800/80 border border-slate-700 text-indigo-400 rounded-3xl flex items-center justify-center mb-4 shadow-inner">
                        <i data-lucide="book-open" class="w-10 h-10"></i>
                    </div>
                    <h3 class="text-lg font-bold text-white mb-1">No lessons found</h3>
                    <p class="text-sm text-slate-400 max-w-sm mb-6">Get started by creating your first professional lesson or try adjusting your search terms.</p>
                    <button onclick="app.openModal()" class="inline-flex items-center space-x-2 bg-indigo-600 hover:bg-indigo-500 text-white px-5 py-2.5 rounded-xl text-sm font-semibold shadow-lg shadow-indigo-600/30 transition-all cursor-pointer">
                        <i data-lucide="plus" class="w-4 h-4"></i>
                        <span>Create Lesson Now</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- View 2: Full Screen Lesson Reader -->
        <div id="reader-view" class="hidden flex-1 flex flex-col overflow-hidden bg-slate-800/60 backdrop-blur-md rounded-3xl border border-slate-700/80 shadow-2xl">
            <!-- Reader Header / Navigation -->
            <div class="px-6 sm:px-8 py-5 border-b border-slate-700/80 flex items-center justify-between bg-slate-800/80">
                <button onclick="app.goHome()" class="inline-flex items-center space-x-2 text-slate-300 hover:text-white font-medium text-sm transition-colors cursor-pointer p-2 rounded-xl hover:bg-slate-700/80">
                    <i data-lucide="arrow-left" class="w-4 h-4"></i>
                    <span>Back to Dashboard</span>
                </button>
                <div class="flex items-center space-x-3">
                    <button id="reader-edit-btn" onclick="app.editCurrentLesson()" class="inline-flex items-center space-x-1.5 px-3.5 py-2 border border-slate-700 bg-slate-800 hover:bg-slate-700 text-slate-200 text-xs font-semibold rounded-xl shadow-sm transition-all cursor-pointer">
                        <i data-lucide="edit-3" class="w-3.5 h-3.5 text-indigo-400"></i>
                        <span>Edit Lesson</span>
                    </button>
                    <button id="reader-delete-btn" onclick="app.deleteCurrentLesson()" class="inline-flex items-center space-x-1.5 px-3.5 py-2 border border-red-500/30 bg-red-500/10 hover:bg-red-500/20 text-red-300 text-xs font-semibold rounded-xl transition-all cursor-pointer">
                        <i data-lucide="trash-2" class="w-3.5 h-3.5"></i>
                        <span>Delete</span>
                    </button>
                </div>
            </div>
            <!-- Reader Content Scroll Area -->
            <div class="flex-1 overflow-y-auto px-6 sm:px-16 py-10 max-w-4xl mx-auto w-full">
                <div class="mb-8">
                    <span id="reader-category" class="inline-block px-3.5 py-1.5 bg-indigo-500/20 text-indigo-300 border border-indigo-500/30 font-bold text-xs rounded-full uppercase tracking-wider mb-4">Category</span>
                    <h2 id="reader-title" class="text-3xl sm:text-4xl font-extrabold text-white tracking-tight mb-4 leading-snug">Lesson Title</h2>
                    <p id="reader-description" class="text-base sm:text-lg text-slate-300 leading-relaxed font-normal">Short description of the lesson goes here.</p>
                </div>
                <hr class="border-slate-700/80 my-8">
                <!-- Rich Content / Steps Area -->
                <div id="reader-content" class="space-y-8">
                    <!-- Dynamic lesson content steps -->
                </div>
            </div>
        </div>

    </main>

    <!-- Modal: Create / Edit Lesson -->
    <div id="lesson-modal" class="fixed inset-0 bg-slate-950/80 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-300">
        <div class="bg-slate-900 border border-slate-700 rounded-3xl shadow-2xl max-w-3xl w-full max-h-[92vh] flex flex-col overflow-hidden transform scale-95 transition-transform duration-300" id="modal-container">
            <div class="px-6 py-5 border-b border-slate-800 flex items-center justify-between bg-slate-800/50">
                <div class="flex items-center space-x-3">
                    <div class="w-10 h-10 rounded-xl bg-indigo-600/20 border border-indigo-500/30 flex items-center justify-center text-indigo-400">
                        <i data-lucide="book-plus" class="w-5 h-5"></i>
                    </div>
                    <h3 id="modal-title" class="font-bold text-lg text-white">Create New Lesson</h3>
                </div>
                <button onclick="app.closeModal()" class="w-9 h-9 rounded-full flex items-center justify-center text-slate-400 hover:text-white hover:bg-slate-800 transition-colors cursor-pointer">
                    <i data-lucide="x" class="w-5 h-5"></i>
                </button>
            </div>
            
            <!-- Professional File Import Dropzone / Bar -->
            <div class="px-6 py-4 bg-gradient-to-r from-indigo-950/40 via-slate-900 to-violet-950/40 border-b border-slate-800 flex flex-col sm:flex-row items-start sm:items-center justify-between gap-3">
                <div class="flex items-center space-x-3 text-xs text-indigo-300 font-medium">
                    <div class="p-2 bg-indigo-500/20 rounded-lg text-indigo-400">
                        <i data-lucide="file-up" class="w-4 h-4"></i>
                    </div>
                    <div>
                        <span class="font-bold text-white block">Instant Multi-Format Import</span>
                        <span>Auto-parse content from PDF, Word (.docx), Video (.mp4), JSON or Text</span>
                    </div>
                </div>
                <label class="inline-flex items-center space-x-2 px-4 py-2 bg-indigo-600 hover:bg-indigo-500 text-white text-xs font-semibold rounded-xl shadow-md transition-all cursor-pointer">
                    <i data-lucide="upload" class="w-4 h-4"></i>
                    <span>Select File to Import</span>
                    <input type="file" id="lesson-file-input" accept=".json,.txt,.md,.pdf,.docx,.mp4,.webm" onchange="app.handleFileImport(event)" class="hidden">
                </label>
            </div>

            <!-- Import Progress Loading Indicator -->
            <div id="import-loading" class="hidden px-6 py-3 bg-indigo-600/10 border-b border-indigo-500/20 text-indigo-300 text-xs flex items-center space-x-3">
                <div class="w-4 h-4 border-2 border-indigo-400 border-t-transparent rounded-full animate-spin"></div>
                <span id="import-loading-text">Parsing file and extracting structured content...</span>
            </div>

            <form id="lesson-form" onsubmit="app.saveLesson(event)" class="flex-1 overflow-y-auto p-6 sm:p-8 space-y-6">
                <input type="hidden" id="lesson-id">
                
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-5">
                    <div>
                        <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider mb-2">Lesson Title *</label>
                        <input type="text" id="form-title" required placeholder="e.g. Advanced Quantum Physics" class="w-full px-4 py-3 bg-slate-800/80 border border-slate-700 rounded-2xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                    </div>
                    <div>
                        <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider mb-2">Category *</label>
                        <input type="text" id="form-category" required placeholder="e.g. Science, Tech, Business" list="category-suggestions" class="w-full px-4 py-3 bg-slate-800/80 border border-slate-700 rounded-2xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <datalist id="category-suggestions">
                            <option value="Science">
                            <option value="Mathematics">
                            <option value="Technology">
                            <option value="Business">
                            <option value="History">
                            <option value="Arts">
                        </datalist>
                    </div>
                </div>

                <div>
                    <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider mb-2">Short Description *</label>
                    <textarea id="form-description" required rows="2" placeholder="Brief summary of what this lesson covers..." class="w-full px-4 py-3 bg-slate-800/80 border border-slate-700 rounded-2xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500"></textarea>
                </div>

                <div>
                    <div class="flex items-center justify-between mb-3">
                        <label class="block text-xs font-bold text-slate-300 uppercase tracking-wider">Lesson Content Steps *</label>
                        <button type="button" onclick="app.addContentBlock()" class="inline-flex items-center space-x-1.5 text-xs font-bold text-indigo-400 hover:text-indigo-300 bg-indigo-500/10 hover:bg-indigo-500/20 px-3 py-1.5 rounded-xl border border-indigo-500/30 transition-all cursor-pointer">
                            <i data-lucide="plus" class="w-3.5 h-3.5"></i>
                            <span>Add Content Step</span>
                        </button>
                    </div>
                    <p class="text-xs text-slate-400 mb-4">Structure your lesson with sequential headings, paragraphs, callout note boxes, or embedded video files.</p>
                    
                    <div id="content-blocks-container" class="space-y-4">
                        <!-- Dynamic content block items -->
                    </div>
                </div>

                <div class="pt-6 border-t border-slate-800 flex items-center justify-end space-x-3">
                    <button type="button" onclick="app.closeModal()" class="px-5 py-2.5 border border-slate-700 hover:bg-slate-800 text-slate-300 text-sm font-semibold rounded-2xl transition-colors cursor-pointer">Cancel</button>
                    <button type="submit" class="px-6 py-2.5 bg-indigo-600 hover:bg-indigo-500 text-white text-sm font-semibold rounded-2xl shadow-lg shadow-indigo-600/30 transition-all cursor-pointer">Save Lesson</button>
                </div>
            </form>
        </div>
    </div>

    <!-- Toast Notification -->
    <div id="toast" class="fixed bottom-6 right-6 z-50 transform translate-y-20 opacity-0 transition-all duration-300 pointer-events-none">
        <div class="bg-slate-800 border border-slate-700 text-white px-5 py-3.5 rounded-2xl shadow-2xl flex items-center space-x-3">
            <div class="w-6 h-6 rounded-full bg-emerald-500/20 text-emerald-400 flex items-center justify-center">
                <i data-lucide="check" class="w-4 h-4"></i>
            </div>
            <span id="toast-message" class="text-sm font-semibold">Action completed successfully</span>
        </div>
    </div>

    <script>
        class LessonApp {
            constructor() {
                this.lessons = [];
                this.currentFilter = 'All';
                this.searchQuery = '';
                this.activeLessonId = null;
                this.initStorage();
                this.loadLessons();
            }

            // Initialize sample professional lessons if local storage is empty
            initStorage() {
                const stored = localStorage.getItem('lesson_hub_pro_data');
                if (!stored) {
                    const sampleLessons = [
                        {
                            id: 'lesson-1',
                            title: 'Advanced Photosynthesis & Energy Dynamics',
                            category: 'Science',
                            description: 'Comprehensive study on how plants convert photons into biochemical energy across light-dependent and Calvin cycles.',
                            content: [
                                { type: 'heading', text: '1. Light-Dependent Reactions' },
                                { type: 'text', text: 'Photosystems II and I absorb solar photons in the thylakoid membrane, initiating electron transport chains that generate ATP and NADPH.' },
                                { type: 'note', text: 'Water photolysis splits H2O molecules to replace excited electrons, releasing atmospheric oxygen as a vital byproduct.' },
                                { type: 'heading', text: '2. The Calvin Cycle (Light-Independent)' },
                                { type: 'text', text: 'Carbon dioxide is fixed into organic sugar molecules utilizing the chemical energy stored in ATP and NADPH produced during phase one.' }
                            ],
                            createdAt: new Date().toISOString()
                        },
                        {
                            id: 'lesson-2',
                            title: 'Modern UI/UX Design Systems & Tokens',
                            category: 'Technology',
                            description: 'Learn how to construct scalable design systems, token architectures, and accessible interactive interfaces.',
                            content: [
                                { type: 'heading', text: 'Introduction to Design Tokens' },
                                { type: 'text', text: 'Design tokens store the visual design attributes such as spacing, color palettes, and typography scales across platforms.' },
                                { type: 'note', text: 'Always prioritize high color contrast ratios and responsive touch targets for mobile accessibility.' }
                            ],
                            createdAt: new Date(Date.now() - 86400000).toISOString()
                        }
                    ];
                    localStorage.setItem('lesson_hub_pro_data', JSON.stringify(sampleLessons));
                }
            }

            loadLessons() {
                try {
                    const data = localStorage.getItem('lesson_hub_pro_data');
                    this.lessons = data ? JSON.parse(data) : [];
                } catch (e) {
                    this.lessons = [];
                }
                this.render();
            }

            saveToStorage() {
                localStorage.setItem('lesson_hub_pro_data', JSON.stringify(this.lessons));
            }

            render() {
                this.renderCategories();
                this.renderLessonsGrid();
                lucide.createIcons();
            }

            renderCategories() {
                const container = document.getElementById('category-filters');
                const categories = ['All', ...new Set(this.lessons.map(l => l.category).filter(Boolean))];
                
                container.innerHTML = categories.map(cat => `
                    <button onclick="app.filterCategory('${cat}')" class="category-btn px-4 py-2.5 rounded-xl text-xs font-semibold whitespace-nowrap transition-all cursor-pointer shadow-md ${this.currentFilter === cat ? 'bg-indigo-600 text-white shadow-indigo-600/30' : 'bg-slate-800 border border-slate-700 text-slate-300 hover:bg-slate-700'}">
                        ${cat}
                    </button>
                `).join('');
            }

            renderLessonsGrid() {
                const grid = document.getElementById('lessons-grid');
                const emptyState = document.getElementById('empty-state');

                let filtered = this.lessons;

                if (this.currentFilter !== 'All') {
                    filtered = filtered.filter(l => l.category.toLowerCase() === this.currentFilter.toLowerCase());
                }

                if (this.searchQuery.trim() !== '') {
                    const q = this.searchQuery.toLowerCase();
                    filtered = filtered.filter(l => 
                        l.title.toLowerCase().includes(q) || 
                        l.category.toLowerCase().includes(q) || 
                        l.description.toLowerCase().includes(q) ||
                        (l.content && l.content.some(c => c.text.toLowerCase().includes(q)))
                    );
                }

                if (filtered.length === 0) {
                    grid.innerHTML = '';
                    emptyState.classList.remove('hidden');
                    return;
                }

                emptyState.classList.add('hidden');

                grid.innerHTML = filtered.map(lesson => {
                    const stepCount = lesson.content ? lesson.content.length : 0;
                    const dateStr = new Date(lesson.createdAt).toLocaleDateString(undefined, { month: 'short', day: 'numeric', year: 'numeric' });
                    
                    return `
                        <div onclick="app.openReader('${lesson.id}')" class="bg-slate-800/80 border border-slate-700/80 rounded-3xl p-6 shadow-xl hover:shadow-2xl hover:border-indigo-500/50 transition-all duration-300 flex flex-col justify-between cursor-pointer group transform hover:-translate-y-1">
                            <div>
                                <div class="flex items-center justify-between mb-4">
                                    <span class="px-3 py-1 bg-indigo-500/20 text-indigo-300 border border-indigo-500/30 font-bold text-xs rounded-full uppercase tracking-wider">${lesson.category}</span>
                                    <span class="text-xs text-slate-400 font-medium">${dateStr}</span>
                                </div>
                                <h3 class="font-bold text-lg text-white group-hover:text-indigo-400 transition-colors mb-2.5 line-clamp-2">${lesson.title}</h3>
                                <p class="text-sm text-slate-300 line-clamp-3 mb-6 leading-relaxed">${lesson.description}</p>
                            </div>
                            <div class="pt-4 border-t border-slate-700/60 flex items-center justify-between text-xs font-semibold text-slate-400">
                                <span class="flex items-center space-x-1.5 bg-slate-900/60 px-3 py-1.5 rounded-xl border border-slate-700/50">
                                    <i data-lucide="layers" class="w-3.5 h-3.5 text-indigo-400"></i>
                                    <span>${stepCount} Step${stepCount === 1 ? '' : 's'}</span>
                                </span>
                                <span class="text-indigo-400 group-hover:translate-x-1 transition-transform inline-flex items-center space-x-1">
                                    <span>Read Lesson</span>
                                    <i data-lucide="arrow-right" class="w-3.5 h-3.5"></i>
                                </span>
                            </div>
                        </div>
                    `;
                }).join('');
            }

            filterCategory(cat) {
                this.currentFilter = cat;
                this.render();
            }

            handleSearch(e) {
                this.searchQuery = e.target.value;
                this.renderLessonsGrid();
                lucide.createIcons();
            }

            openModal(lessonId = null) {
                const modal = document.getElementById('lesson-modal');
                const container = document.getElementById('modal-container');
                const titleEl = document.getElementById('modal-title');
                const form = document.getElementById('lesson-form');
                
                form.reset();
                document.getElementById('content-blocks-container').innerHTML = '';
                const fileInput = document.getElementById('lesson-file-input');
                if (fileInput) fileInput.value = '';
                this.hideImportLoading();

                if (lessonId) {
                    titleEl.textContent = 'Edit Professional Lesson';
                    document.getElementById('lesson-id').value = lessonId;
                    const lesson = this.lessons.find(l => l.id === lessonId);
                    if (lesson) {
                        document.getElementById('form-title').value = lesson.title || '';
                        document.getElementById('form-category').value = lesson.category || '';
                        document.getElementById('form-description').value = lesson.description || '';
                        if (Array.isArray(lesson.content)) {
                            lesson.content.forEach(b => this.addContentBlock(b.type, b.text, b.url));
                        }
                    }
                } else {
                    titleEl.textContent = 'Create New Lesson';
                    document.getElementById('lesson-id').value = '';
                    this.addContentBlock('heading', 'Introduction & Overview');
                    this.addContentBlock('text', 'Write your first core paragraph or step description here...');
                }

                modal.classList.remove('hidden');
                setTimeout(() => {
                    modal.classList.remove('opacity-0');
                    container.classList.remove('scale-95');
                }, 10);
                lucide.createIcons();
            }

            closeModal() {
                const modal = document.getElementById('lesson-modal');
                const container = document.getElementById('modal-container');
                modal.classList.add('opacity-0');
                container.classList.add('scale-95');
                setTimeout(() => {
                    modal.classList.add('hidden');
                }, 300);
            }

            showImportLoading(text = 'Parsing file and extracting structured content...') {
                const el = document.getElementById('import-loading');
                const textEl = document.getElementById('import-loading-text');
                if (textEl) textEl.textContent = text;
                if (el) el.classList.remove('hidden');
            }

            hideImportLoading() {
                const el = document.getElementById('import-loading');
                if (el) el.classList.add('hidden');
            }

            addContentBlock(type = 'text', text = '', url = '') {
                const container = document.getElementById('content-blocks-container');
                const blockId = 'block_' + Math.random().toString(36).substring(2, 9);
                
                const div = document.createElement('div');
                div.className = 'bg-slate-800/90 p-4 rounded-2xl border border-slate-700/80 space-y-3 group';
                div.id = blockId;
                div.innerHTML = `
                    <div class="flex items-center justify-between">
                        <select name="block-type" onchange="app.onBlockTypeChange('${blockId}')" class="text-xs font-bold bg-slate-900 border border-slate-700 rounded-xl px-3 py-1.5 text-indigo-300 focus:outline-none focus:ring-1 focus:ring-indigo-500">
                            <option value="heading" ${type === 'heading' ? 'selected' : ''}>Heading / Chapter Title</option>
                            <option value="text" ${type === 'text' ? 'selected' : ''}>Paragraph Text</option>
                            <option value="note" ${type === 'note' ? 'selected' : ''}>Callout / Note Box</option>
                            <option value="video" ${type === 'video' ? 'selected' : ''}>Embedded Video (.mp4)</option>
                        </select>
                        <button type="button" onclick="document.getElementById('${blockId}').remove()" class="text-slate-400 hover:text-red-400 p-1.5 rounded-xl hover:bg-slate-700/80 transition-colors cursor-pointer" title="Remove block">
                            <i data-lucide="trash-2" class="w-4 h-4"></i>
                        </button>
                    </div>
                    <div class="block-text-wrapper ${type === 'video' ? 'hidden' : ''}">
                        <textarea name="block-text" rows="2" placeholder="Enter step details or text..." class="w-full px-3.5 py-2.5 bg-slate-900 border border-slate-700 rounded-xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500">${text}</textarea>
                    </div>
                    <div class="block-video-wrapper ${type === 'video' ? '' : 'hidden'} space-y-2">
                        <input type="text" name="block-url" placeholder="Video URL or Object URL" value="${url}" class="w-full px-3.5 py-2.5 bg-slate-900 border border-slate-700 rounded-xl text-sm text-slate-100 placeholder-slate-500 focus:outline-none focus:ring-2 focus:ring-indigo-500">
                        <p class="text-[11px] text-slate-400">Video uploaded via file picker will be auto-embedded securely.</p>
                    </div>
                `;
                container.appendChild(div);
                lucide.createIcons();
            }

            onBlockTypeChange(blockId) {
                const blockDiv = document.getElementById(blockId);
                if (!blockDiv) return;
                const select = blockDiv.querySelector('select[name="block-type"]');
                const textWrapper = blockDiv.querySelector('.block-text-wrapper');
                const videoWrapper = blockDiv.querySelector('.block-video-wrapper');
                
                if (select.value === 'video') {
                    textWrapper.classList.add('hidden');
                    videoWrapper.classList.remove('hidden');
                } else {
                    textWrapper.classList.remove('hidden');
                    videoWrapper.classList.add('hidden');
                }
            }

            async handleFileImport(e) {
                const file = e.target.files[0];
                if (!file) return;

                const fileName = file.name.toLowerCase();
                this.showImportLoading(`Parsing ${file.name} (${Math.round(file.size / 1024)} KB)...`);

                try {
                    if (fileName.endsWith('.json')) {
                        const content = await file.text();
                        const parsed = JSON.parse(content);
                        if (parsed.title) document.getElementById('form-title').value = parsed.title;
                        if (parsed.category) document.getElementById('form-category').value = parsed.category;
                        if (parsed.description) document.getElementById('form-description').value = parsed.description;
                        
                        if (Array.isArray(parsed.content) && parsed.content.length > 0) {
                            document.getElementById('content-blocks-container').innerHTML = '';
                            parsed.content.forEach(b => this.addContentBlock(b.type || 'text', b.text || '', b.url || ''));
                        }
                        this.showToast('JSON lesson imported successfully!');
                    } 
                    else if (fileName.endsWith('.pdf')) {
                        const arrayBuffer = await file.arrayBuffer();
                        const loadingTask = window.pdfjsLib.getDocument({ data: arrayBuffer });
                        const pdfDoc = await loadingTask.promise;
                        
                        let extractedText = '';
                        for (let i = 1; i <= pdfDoc.numPages; i++) {
                            const page = await pdfDoc.getPage(i);
                            const textContent = await page.getTextContent();
                            const pageText = textContent.items.map(item => item.str).join(' ');
                            extractedText += `\n\n## Page ${i}\n` + pageText;
                        }

                        this.populateContentFromText(file.name.replace(/\.[^/.]+$/, ""), extractedText);
                        this.showToast('PDF document imported and parsed successfully!');
                    }
                    else if (fileName.endsWith('.docx')) {
                        const arrayBuffer = await file.arrayBuffer();
                        const result = await window.mammoth.extractRawText({ arrayBuffer });
                        this.populateContentFromText(file.name.replace(/\.[^/.]+$/, ""), result.value);
                        this.showToast('Word document imported successfully!');
                    }
                    else if (fileName.endsWith('.mp4') || fileName.endsWith('.webm') || fileName.endsWith('.mov')) {
                        const videoUrl = URL.createObjectURL(file);
                        const titleField = document.getElementById('form-title');
                        if (!titleField.value) {
                            titleField.value = file.name.replace(/\.[^/.]+$/, "").replace(/[-_]/g, ' ');
                        }
                        document.getElementById('form-category').value = document.getElementById('form-category').value || 'Media & Video';
                        document.getElementById('form-description').value = document.getElementById('form-description').value || `Video lesson imported from ${file.name}`;
                        
                        document.getElementById('content-blocks-container').innerHTML = '';
                        this.addContentBlock('heading', 'Video Lecture');
                        this.addContentBlock('video', '', videoUrl);
                        this.addContentBlock('text', 'Review the video above carefully and take detailed notes on key concepts.');
                        this.showToast('Video file successfully attached!');
                    }
                    else {
                        // Text or Markdown
                        const content = await file.text();
                        this.populateContentFromText(file.name.replace(/\.[^/.]+$/, ""), content);
                        this.showToast('Text file imported successfully!');
                    }
                } catch (err) {
                    console.error(err);
                    this.showToast('Error parsing file. Please check format.');
                } finally {
                    this.hideImportLoading();
                    lucide.createIcons();
                }
            }

            populateContentFromText(fallbackTitle, rawText) {
                const titleField = document.getElementById('form-title');
                if (!titleField.value && fallbackTitle) {
                    titleField.value = fallbackTitle.replace(/[-_]/g, ' ');
                }

                const lines = rawText.split(/\r?\n/).map(l => l.trim()).filter(l => l !== '');
                document.getElementById('content-blocks-container').innerHTML = '';

                if (lines.length === 0) {
                    this.addContentBlock('text', rawText);
                    return;
                }

                let currentHeading = 'Introduction';
                let currentParagraphs = [];

                lines.forEach((line) => {
                    if (line.startsWith('#') || line.length < 60 && (line.endsWith(':') || line === line.toUpperCase())) {
                        if (currentParagraphs.length > 0) {
                            this.addContentBlock('text', currentParagraphs.join(' '));
                            currentParagraphs = [];
                        }
                        this.addContentBlock('heading', line.replace(/^#+\s*/, ''));
                    } else if (line.toLowerCase().startsWith('note:') || line.startsWith('>')) {
                        this.addContentBlock('note', line.replace(/^>|\bnoted?:?\s*/i, ''));
                    } else {
                        currentParagraphs.push(line);
                        if (currentParagraphs.length >= 3) {
                            this.addContentBlock('text', currentParagraphs.join(' '));
                            currentParagraphs = [];
                        }
                    }
                });

                if (currentParagraphs.length > 0) {
                    this.addContentBlock('text', currentParagraphs.join(' '));
                }
            }

            saveLesson(e) {
                e.preventDefault();
                const idVal = document.getElementById('lesson-id').value;
                const title = document.getElementById('form-title').value.trim();
                const category = document.getElementById('form-category').value.trim();
                const description = document.getElementById('form-description').value.trim();

                const blockDivs = document.querySelectorAll('#content-blocks-container > div');
                const content = [];
                blockDivs.forEach(div => {
                    const typeSel = div.querySelector('select[name="block-type"]');
                    const textAre = div.querySelector('textarea[name="block-text"]');
                    const urlInput = div.querySelector('input[name="block-url"]');
                    
                    if (typeSel) {
                        content.push({
                            type: typeSel.value,
                            text: textAre ? textAre.value.trim() : '',
                            url: urlInput ? urlInput.value.trim() : ''
                        });
                    }
                });

                if (!title || !category || content.length === 0) {
                    this.showToast('Please fill out all required fields and add at least one step.');
                    return;
                }

                if (idVal) {
                    const index = this.lessons.findIndex(l => l.id === idVal);
                    if (index !== -1) {
                        this.lessons[index] = {
                            ...this.lessons[index],
                            title,
                            category,
                            description,
                            content
                        };
                    }
                    this.showToast('Professional lesson updated successfully!');
                } else {
                    const newLesson = {
                        id: 'lesson_' + Math.random().toString(36).substring(2, 9),
                        title,
                        category,
                        description,
                        content,
                        createdAt: new Date().toISOString()
                    };
                    this.lessons.unshift(newLesson);
                    this.showToast('Professional lesson created successfully!');
                }

                this.saveToStorage();
                this.closeModal();
                this.render();

                if (this.activeLessonId === idVal) {
                    this.openReader(idVal);
                }
            }

            openReader(lessonId) {
                const lesson = this.lessons.find(l => l.id === lessonId);
                if (!lesson) return;

                this.activeLessonId = lessonId;
                document.getElementById('home-view').classList.add('hidden');
                document.getElementById('reader-view').classList.remove('hidden');

                document.getElementById('reader-category').textContent = lesson.category;
                document.getElementById('reader-title').textContent = lesson.title;
                document.getElementById('reader-description').textContent = lesson.description;

                const contentContainer = document.getElementById('reader-content');
                if (Array.isArray(lesson.content) && lesson.content.length > 0) {
                    contentContainer.innerHTML = lesson.content.map((block, idx) => {
                        if (block.type === 'heading') {
                            return `<h3 class="text-xl sm:text-2xl font-bold text-white mt-10 mb-4 flex items-center space-x-3">
                                <span class="text-xs bg-indigo-600/30 border border-indigo-500/40 text-indigo-300 w-7 h-7 rounded-xl inline-flex items-center justify-center font-bold shadow-inner">${idx + 1}</span>
                                <span>${block.text}</span>
                            </h3>`;
                        } else if (block.type === 'note') {
                            return `<div class="bg-amber-500/10 border-l-4 border-amber-400 p-5 rounded-r-2xl my-6 text-amber-200 text-sm sm:text-base leading-relaxed border-y border-r border-amber-500/20 shadow-lg">
                                <div class="font-bold flex items-center space-x-2 mb-2 text-amber-300">
                                    <i data-lucide="info" class="w-4 h-4"></i>
                                    <span>Professional Key Takeaway / Note</span>
                                </div>
                                <p>${block.text}</p>
                            </div>`;
                        } else if (block.type === 'video') {
                            return `<div class="my-6 rounded-2xl overflow-hidden border border-slate-700 bg-slate-900 shadow-2xl">
                                <video controls class="w-full max-h-[480px] object-contain bg-black" src="${block.url}">
                                    Your browser does not support the video tag.
                                </video>
                                <div class="p-3 bg-slate-800/90 text-xs text-slate-400 flex items-center space-x-2">
                                    <i data-lucide="video" class="w-4 h-4 text-indigo-400"></i>
                                    <span>Interactive Lecture Video</span>
                                </div>
                            </div>`;
                        } else {
                            return `<p class="text-base sm:text-lg text-slate-300 leading-relaxed font-normal">${block.text}</p>`;
                        }
                    }).join('');
                } else {
                    contentContainer.innerHTML = `<p class="text-slate-500 italic">No content steps available for this lesson.</p>`;
                }

                window.scrollTo({ top: 0, behavior: 'smooth' });
                lucide.createIcons();
            }

            goHome() {
                this.activeLessonId = null;
                document.getElementById('reader-view').classList.add('hidden');
                document.getElementById('home-view').classList.remove('hidden');
                this.render();
            }

            editCurrentLesson() {
                if (this.activeLessonId) {
                    this.openModal(this.activeLessonId);
                }
            }

            deleteCurrentLesson() {
                if (!this.activeLessonId) return;
                // Custom professional confirmation modal can be simulated or handled cleanly
                if (confirm('Are you sure you want to delete this professional lesson?')) {
                    this.lessons = this.lessons.filter(l => l.id !== this.activeLessonId);
                    this.saveToStorage();
                    this.showToast('Lesson deleted successfully');
                    this.goHome();
                }
            }

            showToast(message) {
                const toast = document.getElementById('toast');
                document.getElementById('toast-message').textContent = message;
                toast.classList.remove('translate-y-20', 'opacity-0');
                setTimeout(() => {
                    toast.classList.add('translate-y-20', 'opacity-0');
                }, 3500);
            }
        }

        // Initialize application globally on DOMContentLoaded
        document.addEventListener('DOMContentLoaded', () => {
            window.app = new LessonApp();
        });
    </script>
</body>
</html>
