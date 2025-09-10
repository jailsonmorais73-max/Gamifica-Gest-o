<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GamificaGestão - Login</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap');
        
        body {
            font-family: 'Inter', sans-serif;
        }
        
        .progress-bar {
            background: linear-gradient(90deg, #10b981 0%, #059669 100%);
            transition: width 0.5s ease-in-out;
        }
        
        .task-card {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .task-card:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }
        
        .department-tab {
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .department-tab:hover {
            transform: translateY(-1px);
        }
        
        .department-tab.active {
            background: linear-gradient(135deg, #3b82f6, #1d4ed8);
            color: white;
        }
        
        .priority-urgent { border-left: 4px solid #ef4444; }
        .priority-important { border-left: 4px solid #f59e0b; }
        .priority-low { border-left: 4px solid #10b981; }
        
        .zone-pending { background: linear-gradient(135deg, #fef2f2, #fee2e2); }
        .zone-progress { background: linear-gradient(135deg, #fffbeb, #fef3c7); }
        .zone-completed { background: linear-gradient(135deg, #f0fdf4, #dcfce7); }
        
        .login-container {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .login-card {
            backdrop-filter: blur(10px);
            background: rgba(255, 255, 255, 0.95);
            border: 1px solid rgba(255, 255, 255, 0.2);
        }
        
        .floating-shapes {
            position: absolute;
            width: 100%;
            height: 100%;
            overflow: hidden;
            z-index: 0;
        }
        
        .shape {
            position: absolute;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            animation: float 6s ease-in-out infinite;
        }
        
        .shape:nth-child(1) { width: 80px; height: 80px; top: 20%; left: 10%; animation-delay: 0s; }
        .shape:nth-child(2) { width: 120px; height: 120px; top: 60%; right: 10%; animation-delay: 2s; }
        .shape:nth-child(3) { width: 60px; height: 60px; bottom: 20%; left: 20%; animation-delay: 4s; }
        
        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }
        
        /* Responsividade para o painel lateral */
        @media (max-width: 768px) {
            #sidebar {
                position: fixed;
                top: 0;
                left: 0;
                height: 100vh;
                z-index: 40;
            }
            
            #sidebar.mobile-hidden {
                transform: translateX(-100%);
            }
            
            #mainContent {
                margin-left: 0 !important;
            }
            
            #toggleSidebar {
                z-index: 50;
            }
        }
    </style>
</head>
<body>
    <!-- Tela de Login -->
    <div id="loginScreen" class="login-container flex items-center justify-center relative">
        <div class="floating-shapes">
            <div class="shape"></div>
            <div class="shape"></div>
            <div class="shape"></div>
        </div>
        
        <div class="login-card rounded-2xl shadow-2xl p-8 w-full max-w-md mx-4 relative z-10">
            <div class="text-center mb-8">
                <h1 class="text-3xl font-bold text-gray-800 mb-2">🎮 GamificaGestão</h1>
                <p class="text-gray-600">Faça login para acessar seu painel</p>
            </div>
            
            <form onsubmit="handleLogin(event)" class="space-y-6">
                <div>
                    <label for="employeeId" class="block text-sm font-medium text-gray-700 mb-2">
                        👤 ID do Colaborador
                    </label>
                    <input 
                        type="text" 
                        id="employeeId" 
                        name="employeeId"
                        placeholder="Digite seu ID (ex: FIN001, MKT002, TEC003)"
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all"
                        required
                    >
                </div>
                
                <div>
                    <label for="password" class="block text-sm font-medium text-gray-700 mb-2">
                        🔒 Senha
                    </label>
                    <div class="relative">
                        <input 
                            type="password" 
                            id="password" 
                            name="password"
                            placeholder="Digite sua senha"
                            class="w-full px-4 py-3 pr-12 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent transition-all"
                            required
                        >
                        <button 
                            type="button" 
                            onclick="togglePassword()" 
                            class="absolute right-3 top-1/2 transform -translate-y-1/2 text-gray-500 hover:text-gray-700 transition-colors"
                        >
                            <span id="eyeIcon">👁️</span>
                        </button>
                    </div>
                </div>
                
                <button 
                    type="submit" 
                    class="w-full bg-gradient-to-r from-blue-500 to-purple-600 hover:from-blue-600 hover:to-purple-700 text-white font-semibold py-3 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg"
                >
                    🚀 Entrar no Sistema
                </button>
                
                <div class="text-center">
                    <button 
                        type="button" 
                        onclick="openForgotPasswordModal()" 
                        class="text-sm text-blue-600 hover:text-blue-800 transition-colors underline"
                    >
                        🔑 Esqueceu a senha?
                    </button>
                </div>
            </form>
            
            <div class="mt-6 text-center">
                <p class="text-sm text-gray-600 mb-4">IDs de exemplo para teste:</p>
                <div class="grid grid-cols-2 gap-2 text-xs">
                    <div class="bg-blue-50 p-2 rounded">💰 FIN001</div>
                    <div class="bg-green-50 p-2 rounded">📈 MKT002</div>
                    <div class="bg-purple-50 p-2 rounded">💻 TEC003</div>
                    <div class="bg-yellow-50 p-2 rounded">👥 RH004</div>
                </div>
                <p class="text-xs text-gray-500 mt-2">Senha: 123456 (para todos)</p>
            </div>
        </div>
    </div>

    <!-- Painel de Seleção de Departamentos -->
    <div id="departmentSelectionScreen" class="hidden bg-gradient-to-br from-purple-600 via-blue-600 to-indigo-700 min-h-screen flex items-center justify-center relative">
        <div class="floating-shapes">
            <div class="shape"></div>
            <div class="shape"></div>
            <div class="shape"></div>
        </div>
        
        <div class="bg-white rounded-3xl shadow-2xl p-8 w-full max-w-4xl mx-4 relative z-10">
            <div class="text-center mb-8">
                <h1 class="text-3xl font-bold text-gray-800 mb-2">🏢 Selecione seu Departamento</h1>
                <p class="text-gray-600">Olá, <span id="welcomeUserName" class="font-semibold text-blue-600"></span>! Escolha seu departamento para acessar o painel</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6" id="departmentCards">
                <!-- Financeiro -->
                <div class="department-card bg-gradient-to-br from-blue-50 to-blue-100 p-6 rounded-2xl border-2 border-blue-200 hover:border-blue-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Financeiro')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">💰</div>
                        <h3 class="text-xl font-bold text-blue-800 mb-2">Financeiro</h3>
                        <p class="text-sm text-blue-600 mb-4">Gestão financeira e contábil</p>
                        <div class="bg-blue-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>

                <!-- Marketing -->
                <div class="department-card bg-gradient-to-br from-green-50 to-green-100 p-6 rounded-2xl border-2 border-green-200 hover:border-green-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Marketing')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">📈</div>
                        <h3 class="text-xl font-bold text-green-800 mb-2">Marketing</h3>
                        <p class="text-sm text-green-600 mb-4">Campanhas e estratégias</p>
                        <div class="bg-green-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>

                <!-- Tecnologia -->
                <div class="department-card bg-gradient-to-br from-purple-50 to-purple-100 p-6 rounded-2xl border-2 border-purple-200 hover:border-purple-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Tecnologia')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">💻</div>
                        <h3 class="text-xl font-bold text-purple-800 mb-2">Tecnologia</h3>
                        <p class="text-sm text-purple-600 mb-4">Desenvolvimento e TI</p>
                        <div class="bg-purple-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>

                <!-- Recursos Humanos -->
                <div class="department-card bg-gradient-to-br from-yellow-50 to-yellow-100 p-6 rounded-2xl border-2 border-yellow-200 hover:border-yellow-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Recursos Humanos')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">👥</div>
                        <h3 class="text-xl font-bold text-yellow-800 mb-2">Recursos Humanos</h3>
                        <p class="text-sm text-yellow-600 mb-4">Gestão de pessoas</p>
                        <div class="bg-yellow-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>

                <!-- Administrativo -->
                <div class="department-card bg-gradient-to-br from-gray-50 to-gray-100 p-6 rounded-2xl border-2 border-gray-200 hover:border-gray-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Administrativo')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">📋</div>
                        <h3 class="text-xl font-bold text-gray-800 mb-2">Administrativo</h3>
                        <p class="text-sm text-gray-600 mb-4">Processos e documentação</p>
                        <div class="bg-gray-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>

                <!-- Vendas -->
                <div class="department-card bg-gradient-to-br from-red-50 to-red-100 p-6 rounded-2xl border-2 border-red-200 hover:border-red-400 cursor-pointer transition-all duration-300 transform hover:scale-105 hover:shadow-xl" onclick="selectDepartment('Vendas')">
                    <div class="text-center">
                        <div class="text-6xl mb-4">🏪</div>
                        <h3 class="text-xl font-bold text-red-800 mb-2">Vendas</h3>
                        <p class="text-sm text-red-600 mb-4">Comercial e negócios</p>
                        <div class="bg-red-500 text-white px-4 py-2 rounded-lg font-semibold">
                            Acessar Painel
                        </div>
                    </div>
                </div>
            </div>

            <div class="text-center mt-8">
                <button onclick="backToLogin()" class="text-gray-500 hover:text-gray-700 transition-colors underline">
                    ← Voltar ao Login
                </button>
            </div>
        </div>
    </div>

    <!-- Painel Principal (inicialmente oculto) -->
    <div id="mainPanel" class="hidden bg-gradient-to-br from-indigo-50 via-white to-purple-50 min-h-screen flex">
        <!-- Botão Toggle do Painel -->
        <button 
            id="toggleSidebar" 
            onclick="toggleSidebar()" 
            class="fixed top-4 left-4 z-50 bg-indigo-600 hover:bg-indigo-700 text-white p-3 rounded-full shadow-lg transition-all duration-300 transform hover:scale-110"
            title="Abrir/Fechar Painel de Controle"
        >
            <span id="toggleIcon">📊</span>
        </button>

        <!-- Barra Lateral -->
        <div id="sidebar" class="w-80 bg-white shadow-2xl border-r-4 border-indigo-500 flex flex-col transition-transform duration-300 transform translate-x-0">
            <div class="p-6 border-b border-gray-200">
                <div class="flex items-center justify-between">
                    <h2 class="text-xl font-bold text-gray-800 flex items-center">
                        📊 Painel de Controle
                    </h2>
                    <button onclick="logout()" class="text-sm text-red-600 hover:text-red-800 transition-colors">
                        🚪 Sair
                    </button>
                </div>
                <div class="mt-2">
                    <p class="text-sm text-gray-600">Bem-vindo(a), <span id="userName" class="font-semibold"></span></p>
                    <p class="text-xs text-gray-500"><span id="userDepartment"></span></p>
                </div>
            </div>
            
            <div class="flex-1 p-6 space-y-6">
                <!-- Relatório Mensal -->
                <div class="bg-gradient-to-br from-blue-50 to-indigo-50 p-6 rounded-xl border border-blue-200">
                    <h3 class="text-lg font-semibold text-blue-800 mb-4 flex items-center">
                        📈 Relatório Mensal
                    </h3>
                    
                    <!-- Seletor de Mês -->
                    <div class="mb-4">
                        <label class="block text-sm font-medium text-blue-700 mb-2">📅 Selecionar Mês:</label>
                        <select id="monthSelector" onchange="changeMonth()" class="w-full px-3 py-2 border border-blue-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent bg-white text-sm">
                            <option value="2024-12">🎄 Dezembro 2024</option>
                            <option value="2024-11">🍂 Novembro 2024</option>
                            <option value="2024-10">🎃 Outubro 2024</option>
                            <option value="2024-09">🍁 Setembro 2024</option>
                            <option value="2024-08">☀️ Agosto 2024</option>
                            <option value="2024-07">🏖️ Julho 2024</option>
                            <option value="2024-06">🌻 Junho 2024</option>
                            <option value="2024-05">🌸 Maio 2024</option>
                            <option value="2024-04">🌷 Abril 2024</option>
                            <option value="2024-03">🌱 Março 2024</option>
                            <option value="2024-02">💝 Fevereiro 2024</option>
                            <option value="2024-01">🎊 Janeiro 2024</option>
                        </select>
                    </div>
                    
                    <button onclick="generateMonthlyReport()" class="w-full bg-gradient-to-r from-blue-500 to-blue-600 hover:from-blue-600 hover:to-blue-700 text-white font-semibold py-3 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg">
                        🎯 Gerar Relatório <span id="selectedMonthName">Dezembro</span>
                    </button>
                    
                    <div class="mt-4 space-y-3">
                        <div class="flex justify-between items-center">
                            <span class="text-sm text-gray-600">Meta Mensal:</span>
                            <span class="font-bold text-blue-600" id="monthlyGoal">150 tarefas</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-sm text-gray-600">Concluídas:</span>
                            <span class="font-bold text-green-600" id="monthlyCompleted">127 tarefas</span>
                        </div>
                        <div class="flex justify-between items-center">
                            <span class="text-sm text-gray-600">Taxa de Sucesso:</span>
                            <span class="font-bold text-purple-600" id="successRate">84.7%</span>
                        </div>
                    </div>
                </div>

                <!-- Estatísticas Rápidas -->
                <div class="bg-gradient-to-br from-green-50 to-emerald-50 p-6 rounded-xl border border-green-200">
                    <h3 class="text-lg font-semibold text-green-800 mb-4 flex items-center">
                        ⚡ Estatísticas Rápidas
                    </h3>
                    <div class="space-y-3">
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-600">🔥 Sequência Atual:</span>
                            <span class="bg-orange-100 text-orange-800 px-2 py-1 rounded-full text-sm font-bold" id="currentStreak">7 dias</span>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-600">⭐ Pontuação:</span>
                            <span class="bg-yellow-100 text-yellow-800 px-2 py-1 rounded-full text-sm font-bold" id="userScore">2,847 pts</span>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-600">🏆 Ranking:</span>
                            <span class="bg-purple-100 text-purple-800 px-2 py-1 rounded-full text-sm font-bold" id="userRanking">#3 da equipe</span>
                        </div>
                    </div>
                </div>

                <!-- Funcionários com melhores desempenhos -->
                <div class="bg-gradient-to-br from-purple-50 to-pink-50 p-6 rounded-xl border border-purple-200">
                    <h3 class="text-lg font-semibold text-purple-800 mb-4 flex items-center">
                        🏆 Funcionários com melhores desempenhos
                    </h3>
                    <div class="space-y-2" id="topEmployees">
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <span class="text-lg">🥇</span>
                                <span class="text-sm font-medium">Ana Silva</span>
                            </div>
                            <span class="text-xs bg-gold-100 text-yellow-800 px-2 py-1 rounded font-bold">3,250 pts</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <span class="text-lg">🥈</span>
                                <span class="text-sm font-medium">Carlos Santos</span>
                            </div>
                            <span class="text-xs bg-gray-100 text-gray-800 px-2 py-1 rounded font-bold">2,847 pts</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <span class="text-lg">🥉</span>
                                <span class="text-sm font-medium">Maria Oliveira</span>
                            </div>
                            <span class="text-xs bg-orange-100 text-orange-800 px-2 py-1 rounded font-bold">2,654 pts</span>
                        </div>
                    </div>
                </div>

                <!-- Departamentos com melhores desempenhos -->
                <div class="bg-gradient-to-br from-orange-50 to-red-50 p-6 rounded-xl border border-orange-200">
                    <h3 class="text-lg font-semibold text-orange-800 mb-4 flex items-center">
                        🏢 Departamentos com melhores desempenhos
                    </h3>
                    <div class="space-y-2" id="departmentPerformance">
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <span class="text-sm">💰 Financeiro</span>
                            <span class="text-xs bg-blue-100 text-blue-800 px-2 py-1 rounded">92%</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <span class="text-sm">📈 Marketing</span>
                            <span class="text-xs bg-green-100 text-green-800 px-2 py-1 rounded">88%</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <span class="text-sm">💻 Tecnologia</span>
                            <span class="text-xs bg-purple-100 text-purple-800 px-2 py-1 rounded">85%</span>
                        </div>
                    </div>
                </div>

                <!-- Gestão de Tarefas e Departamentos (apenas para gestores) -->
                <div id="managementSection" class="bg-gradient-to-br from-red-50 to-pink-50 p-6 rounded-xl border border-red-200">
                    <h3 class="text-lg font-semibold text-red-800 mb-4 flex items-center">
                        🎯 Gestão de Tarefas
                    </h3>
                    <div class="space-y-2">
                        <button onclick="openTaskModal()" class="w-full bg-gradient-to-r from-red-500 to-red-600 hover:from-red-600 hover:to-red-700 text-white font-semibold py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg text-sm">
                            ➕ Adicionar Tarefa
                        </button>
                        <button onclick="openDepartmentModal()" class="w-full bg-gradient-to-r from-orange-500 to-orange-600 hover:from-orange-600 hover:to-orange-700 text-white font-semibold py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg text-sm">
                            🏢 Gerenciar Departamentos
                        </button>
                        <button onclick="openAssignModal()" class="w-full bg-gradient-to-r from-purple-500 to-purple-600 hover:from-purple-600 hover:to-purple-700 text-white font-semibold py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg text-sm">
                            👥 Atribuir Tarefas
                        </button>
                        <button onclick="openEmployeeModal()" class="w-full bg-gradient-to-r from-blue-500 to-blue-600 hover:from-blue-600 hover:to-blue-700 text-white font-semibold py-2 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg text-sm">
                            👤 Adicionar Colaborador
                        </button>
                    </div>
                </div>

                <!-- Usuários Online em Tempo Real -->
                <div class="bg-gradient-to-br from-green-50 to-teal-50 p-6 rounded-xl border border-green-200">
                    <h3 class="text-lg font-semibold text-green-800 mb-4 flex items-center">
                        🟢 Usuários Online
                        <span class="ml-2 bg-green-100 text-green-800 px-2 py-1 rounded-full text-xs font-bold" id="onlineCount">4</span>
                    </h3>
                    <div class="space-y-2" id="onlineUsers">
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                                <span class="text-sm font-medium">Ana Silva</span>
                            </div>
                            <span class="text-xs text-gray-500">💰 Financeiro</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                                <span class="text-sm font-medium">Carlos Santos</span>
                            </div>
                            <span class="text-xs text-gray-500">📈 Marketing</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                                <span class="text-sm font-medium">Maria Oliveira</span>
                            </div>
                            <span class="text-xs text-gray-500">💻 Tecnologia</span>
                        </div>
                        <div class="flex items-center justify-between p-2 bg-white rounded-lg">
                            <div class="flex items-center space-x-2">
                                <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                                <span class="text-sm font-medium">João Costa</span>
                            </div>
                            <span class="text-xs text-gray-500">👥 RH</span>
                        </div>
                    </div>
                    <div class="mt-3 text-center">
                        <p class="text-xs text-gray-500">Atualizado há <span id="lastUpdate">2 segundos</span></p>
                    </div>
                </div>

                <!-- Edição de Perfil -->
                <div class="bg-gradient-to-br from-indigo-50 to-blue-50 p-6 rounded-xl border border-indigo-200">
                    <h3 class="text-lg font-semibold text-indigo-800 mb-4 flex items-center">
                        👤 Edição de Perfil
                    </h3>
                    <button onclick="openProfileModal()" class="w-full bg-gradient-to-r from-indigo-500 to-indigo-600 hover:from-indigo-600 hover:to-indigo-700 text-white font-semibold py-3 px-4 rounded-lg transition-all duration-300 transform hover:scale-105 shadow-lg">
                        ⚙️ Editar Perfil
                    </button>
                    
                    <div class="mt-4 space-y-2">
                        <div class="flex items-center justify-center">
                            <div class="w-16 h-16 bg-gray-200 rounded-full flex items-center justify-center text-2xl" id="profilePicPreview">
                                👤
                            </div>
                        </div>
                        <div class="text-center">
                            <p class="text-sm text-gray-600">Foto do Perfil</p>
                            <p class="text-xs text-gray-500">Clique em "Editar Perfil" para alterar</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Conteúdo Principal -->
        <div id="mainContent" class="flex-1 overflow-auto transition-all duration-300">
            <!-- Header do Departamento -->
            <div class="bg-white shadow-lg border-b-4 border-indigo-500">
                <div class="max-w-7xl mx-auto px-6 py-4">
                    <div class="flex items-center justify-between">
                        <div class="flex items-center space-x-4">
                            <button onclick="backToDepartmentSelection()" class="text-gray-500 hover:text-gray-700 transition-colors">
                                ← Voltar aos Departamentos
                            </button>
                            <div class="h-6 w-px bg-gray-300"></div>
                            <h1 class="text-3xl font-bold text-gray-800 flex items-center">
                                🎮 GamificaGestão - <span id="currentDepartmentTitle" class="text-blue-600">Departamento</span>
                            </h1>
                        </div>
                        <div class="text-right">
                            <p class="text-sm text-gray-600">Painel do Departamento</p>
                            <p class="text-lg font-semibold text-blue-600" id="departmentName">Carregando...</p>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Tarefas do Mês -->
            <div class="max-w-7xl mx-auto px-6 py-8">
                <div class="bg-white rounded-2xl shadow-xl p-6 mb-8">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6 flex items-center">
                        📅 Tarefas do Mês - <span id="currentMonthTitle">Dezembro 2024</span>
                    </h2>
                    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-4" id="monthlyTasks">
                        <!-- As tarefas serão carregadas dinamicamente pelo JavaScript -->
                    </div>
                </div>

                <!-- Zonas de Status das Tarefas -->
                <div class="grid grid-cols-1 lg:grid-cols-3 gap-6 mb-8">
                    <!-- Tarefas Pendentes -->
                    <div class="zone-pending rounded-2xl shadow-xl p-6 border-l-4 border-red-500">
                        <h3 class="text-xl font-bold text-red-700 mb-4 flex items-center">
                            😰 Pendentes (3)
                        </h3>
                        <div class="space-y-3" id="pendingTasks">
                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-red-500">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium">Aprovação Orçamento 2025</span>
                                    <button onclick="moveTask(this, 'progress')" class="bg-yellow-500 hover:bg-yellow-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                                        ▶️ Iniciar
                                    </button>
                                </div>
                                <span class="text-xs text-gray-500">😰 Urgente - Prazo: 15/12</span>
                            </div>

                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-yellow-500">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium">Avaliação Performance</span>
                                    <button onclick="moveTask(this, 'progress')" class="bg-yellow-500 hover:bg-yellow-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                                        ▶️ Iniciar
                                    </button>
                                </div>
                                <span class="text-xs text-gray-500">😐 Importante - Prazo: 23/12</span>
                            </div>

                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-green-500">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium">Treinamento Equipe</span>
                                    <button onclick="moveTask(this, 'progress')" class="bg-yellow-500 hover:bg-yellow-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                                        ▶️ Iniciar
                                    </button>
                                </div>
                                <span class="text-xs text-gray-500">😊 Normal - Prazo: 29/12</span>
                            </div>
                        </div>
                    </div>

                    <!-- Tarefas em Andamento -->
                    <div class="zone-progress rounded-2xl shadow-xl p-6 border-l-4 border-yellow-500">
                        <h3 class="text-xl font-bold text-yellow-700 mb-4 flex items-center">
                            😐 Em Andamento (2)
                        </h3>
                        <div class="space-y-3" id="progressTasks">
                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-yellow-500">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium">Deploy Nova Versão</span>
                                    <button onclick="moveTask(this, 'completed')" class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                                        ✅ Concluir
                                    </button>
                                </div>
                                <div class="mt-2 bg-gray-200 rounded-full h-2">
                                    <div class="bg-yellow-500 h-2 rounded-full" style="width: 55%"></div>
                                </div>
                                <span class="text-xs text-gray-600">55% concluído</span>
                            </div>

                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-green-500">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium">Documentação API</span>
                                    <button onclick="moveTask(this, 'completed')" class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                                        ✅ Concluir
                                    </button>
                                </div>
                                <div class="mt-2 bg-gray-200 rounded-full h-2">
                                    <div class="bg-yellow-500 h-2 rounded-full" style="width: 85%"></div>
                                </div>
                                <span class="text-xs text-gray-600">85% concluído</span>
                            </div>
                        </div>
                    </div>

                    <!-- Tarefas Concluídas -->
                    <div class="zone-completed rounded-2xl shadow-xl p-6 border-l-4 border-green-500">
                        <h3 class="text-xl font-bold text-green-700 mb-4 flex items-center">
                            😊 Concluídas (2)
                        </h3>
                        <div class="space-y-3" id="completedTasks">
                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-green-500 opacity-75">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium line-through">Fechamento Mensal</span>
                                    <span class="text-green-600 font-bold">✅</span>
                                </div>
                                <span class="text-xs text-gray-500">🎉 Concluído às 14:30</span>
                            </div>

                            <div class="bg-white p-4 rounded-lg shadow-sm border-l-4 border-green-500 opacity-75">
                                <div class="flex items-center justify-between">
                                    <span class="font-medium line-through">Pagamento Fornecedores</span>
                                    <span class="text-green-600 font-bold">✅</span>
                                </div>
                                <span class="text-xs text-gray-500">🎉 Concluído às 16:45</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Controle de Desenvolvimento Diário -->
                <div class="bg-white rounded-2xl shadow-xl p-8 text-center">
                    <h2 class="text-2xl font-bold text-gray-800 mb-6">📊 Progresso do Dia</h2>
                    <div class="max-w-md mx-auto">
                        <div class="relative">
                            <div class="bg-gray-200 rounded-full h-8 mb-4">
                                <div id="dailyProgress" class="progress-bar h-8 rounded-full flex items-center justify-center text-white font-bold" style="width: 28.5%">
                                    28.5%
                                </div>
                            </div>
                            <div class="flex justify-between text-sm text-gray-600 mb-4">
                                <span>0%</span>
                                <span>50%</span>
                                <span>100%</span>
                            </div>
                        </div>
                        <div class="grid grid-cols-3 gap-4 text-center">
                            <div class="bg-red-50 p-4 rounded-lg">
                                <div class="text-2xl font-bold text-red-600" id="pendingCount">3</div>
                                <div class="text-sm text-red-600">😰 Pendentes</div>
                            </div>
                            <div class="bg-yellow-50 p-4 rounded-lg">
                                <div class="text-2xl font-bold text-yellow-600" id="progressCount">2</div>
                                <div class="text-sm text-yellow-600">😐 Em Andamento</div>
                            </div>
                            <div class="bg-green-50 p-4 rounded-lg">
                                <div class="text-2xl font-bold text-green-600" id="completedCount">2</div>
                                <div class="text-sm text-green-600">😊 Concluídas</div>
                            </div>
                        </div>
                        <div class="mt-6 text-lg font-semibold text-gray-700">
                            🎯 Meta: 7 tarefas | Concluídas: <span id="completedTotal">2</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Edição de Perfil -->
    <div id="profileModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">👤 Editar Perfil</h2>
                <button onclick="closeProfileModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <!-- Foto do Perfil -->
                <div class="text-center">
                    <div class="w-32 h-32 bg-gray-200 rounded-full flex items-center justify-center text-4xl mx-auto mb-4" id="profilePicDisplay">
                        👤
                    </div>
                    <div class="space-y-2">
                        <input type="file" id="profilePicInput" accept="image/*" class="hidden" onchange="handleProfilePicChange(event)">
                        <button onclick="document.getElementById('profilePicInput').click()" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg transition-colors">
                            📷 Alterar Foto
                        </button>
                        <button onclick="removeProfilePic()" class="bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg transition-colors ml-2">
                            🗑️ Remover Foto
                        </button>
                    </div>
                </div>

                <!-- Informações Pessoais -->
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">👤 Nome Completo</label>
                        <input type="text" id="profileName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">📧 Email</label>
                        <input type="email" id="profileEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">📱 Telefone</label>
                        <input type="tel" id="profilePhone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">🏢 Departamento</label>
                        <input type="text" id="profileDepartment" class="w-full px-4 py-3 border border-gray-300 rounded-lg bg-gray-100" readonly>
                    </div>
                </div>

                <!-- Alteração de Senha -->
                <div class="bg-gray-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-gray-800 mb-4">🔒 Alterar Senha</h3>
                    <div class="space-y-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Senha Atual</label>
                            <input type="password" id="currentPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Nova Senha</label>
                            <input type="password" id="newPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">Confirmar Nova Senha</label>
                            <input type="password" id="confirmPassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                        </div>
                    </div>
                </div>

                <!-- Preferências -->
                <div class="bg-blue-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-blue-800 mb-4">⚙️ Preferências</h3>
                    <div class="space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-700">📧 Receber notificações por email</span>
                            <input type="checkbox" id="emailNotifications" class="w-5 h-5 text-blue-600 rounded">
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-700">🔔 Notificações de tarefas</span>
                            <input type="checkbox" id="taskNotifications" class="w-5 h-5 text-blue-600 rounded" checked>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="text-sm text-gray-700">🏆 Notificações de conquistas</span>
                            <input type="checkbox" id="achievementNotifications" class="w-5 h-5 text-blue-600 rounded" checked>
                        </div>
                    </div>
                </div>

                <!-- Botões de Ação -->
                <div class="flex justify-end space-x-4 pt-4">
                    <button onclick="closeProfileModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ❌ Cancelar
                    </button>
                    <button onclick="saveProfile()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-2 rounded-lg transition-colors">
                        💾 Salvar Alterações
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Adicionar Tarefa -->
    <div id="taskModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">➕ Adicionar Nova Tarefa</h2>
                <button onclick="closeTaskModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">📝 Nome da Tarefa</label>
                        <input type="text" id="taskName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-transparent" placeholder="Digite o nome da tarefa">
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">🏢 Departamento</label>
                        <select id="taskDepartment" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-transparent">
                            <option value="">Selecione o departamento</option>
                            <option value="Financeiro">💰 Financeiro</option>
                            <option value="Marketing">📈 Marketing</option>
                            <option value="Tecnologia">💻 Tecnologia</option>
                            <option value="Recursos Humanos">👥 Recursos Humanos</option>
                            <option value="Administrativo">📋 Administrativo</option>
                            <option value="Vendas">🏪 Vendas</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">⚡ Prioridade</label>
                        <select id="taskPriority" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-transparent">
                            <option value="low">😊 Normal</option>
                            <option value="important">😐 Importante</option>
                            <option value="urgent">😰 Urgente</option>
                        </select>
                    </div>
                    <div>
                        <label class="block text-sm font-medium text-gray-700 mb-2">📅 Data de Vencimento</label>
                        <input type="date" id="taskDueDate" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-transparent">
                    </div>
                </div>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">📄 Descrição</label>
                    <textarea id="taskDescription" rows="3" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-red-500 focus:border-transparent" placeholder="Descreva os detalhes da tarefa"></textarea>
                </div>
                
                <div class="flex justify-end space-x-4 pt-4">
                    <button onclick="closeTaskModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ❌ Cancelar
                    </button>
                    <button onclick="saveTask()" class="bg-red-500 hover:bg-red-600 text-white px-6 py-2 rounded-lg transition-colors">
                        💾 Criar Tarefa
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Gerenciar Departamentos -->
    <div id="departmentModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-4xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">🏢 Gerenciar Departamentos</h2>
                <button onclick="closeDepartmentModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <!-- Adicionar Novo Departamento -->
                <div class="bg-orange-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-orange-800 mb-4">➕ Adicionar Novo Departamento</h3>
                    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">🏢 Nome do Departamento</label>
                            <input type="text" id="newDeptName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" placeholder="Ex: Qualidade">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">🎨 Ícone</label>
                            <input type="text" id="newDeptIcon" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-orange-500 focus:border-transparent" placeholder="Ex: 🔍">
                        </div>
                        <div class="flex items-end">
                            <button onclick="addDepartment()" class="w-full bg-orange-500 hover:bg-orange-600 text-white px-4 py-3 rounded-lg transition-colors">
                                ➕ Adicionar
                            </button>
                        </div>
                    </div>
                </div>

                <!-- Lista de Departamentos Existentes -->
                <div>
                    <h3 class="text-lg font-semibold text-gray-800 mb-4">📋 Departamentos Existentes</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4" id="departmentsList">
                        <div class="bg-blue-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">💰 Financeiro</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Financeiro')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Financeiro')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                        <div class="bg-green-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">📈 Marketing</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Marketing')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Marketing')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                        <div class="bg-purple-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">💻 Tecnologia</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Tecnologia')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Tecnologia')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                        <div class="bg-yellow-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">👥 Recursos Humanos</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Recursos Humanos')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Recursos Humanos')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                        <div class="bg-gray-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">📋 Administrativo</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Administrativo')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Administrativo')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                        <div class="bg-red-50 p-4 rounded-lg flex items-center justify-between">
                            <span class="font-medium">🏪 Vendas</span>
                            <div class="space-x-2">
                                <button onclick="editDepartment('Vendas')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                                <button onclick="deleteDepartment('Vendas')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                            </div>
                        </div>
                    </div>
                </div>
                
                <div class="flex justify-end pt-4">
                    <button onclick="closeDepartmentModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ✅ Concluído
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Atribuir Tarefas -->
    <div id="assignModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-3xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">👥 Atribuir Tarefas aos Funcionários</h2>
                <button onclick="closeAssignModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <!-- Seleção de Tarefa -->
                    <div>
                        <h3 class="text-lg font-semibold text-purple-800 mb-4">📝 Selecionar Tarefa</h3>
                        <div class="space-y-2 max-h-64 overflow-y-auto" id="availableTasks">
                            <div class="bg-red-50 p-3 rounded-lg border-l-4 border-red-500 cursor-pointer hover:bg-red-100 task-option" onclick="selectTask(this, 'Relatório Financeiro Q4')">
                                <div class="font-medium">😰 Relatório Financeiro Q4</div>
                                <div class="text-sm text-gray-600">Financeiro - Urgente</div>
                            </div>
                            <div class="bg-yellow-50 p-3 rounded-lg border-l-4 border-yellow-500 cursor-pointer hover:bg-yellow-100 task-option" onclick="selectTask(this, 'Campanha Black Friday')">
                                <div class="font-medium">😐 Campanha Black Friday</div>
                                <div class="text-sm text-gray-600">Marketing - Importante</div>
                            </div>
                            <div class="bg-red-50 p-3 rounded-lg border-l-4 border-red-500 cursor-pointer hover:bg-red-100 task-option" onclick="selectTask(this, 'Correção Bug Crítico')">
                                <div class="font-medium">😰 Correção Bug Crítico</div>
                                <div class="text-sm text-gray-600">Tecnologia - Urgente</div>
                            </div>
                            <div class="bg-green-50 p-3 rounded-lg border-l-4 border-green-500 cursor-pointer hover:bg-green-100 task-option" onclick="selectTask(this, 'Treinamento Equipe')">
                                <div class="font-medium">😊 Treinamento Equipe</div>
                                <div class="text-sm text-gray-600">RH - Normal</div>
                            </div>
                        </div>
                    </div>

                    <!-- Seleção de Funcionário -->
                    <div>
                        <h3 class="text-lg font-semibold text-purple-800 mb-4">👤 Selecionar Funcionário</h3>
                        <div class="space-y-2 max-h-64 overflow-y-auto" id="availableEmployees">
                            <div class="bg-blue-50 p-3 rounded-lg cursor-pointer hover:bg-blue-100 employee-option" onclick="selectEmployee(this, 'Ana Silva', 'FIN001')">
                                <div class="font-medium">Ana Silva (FIN001)</div>
                                <div class="text-sm text-gray-600">💰 Financeiro - 3,250 pts</div>
                            </div>
                            <div class="bg-green-50 p-3 rounded-lg cursor-pointer hover:bg-green-100 employee-option" onclick="selectEmployee(this, 'Carlos Santos', 'MKT002')">
                                <div class="font-medium">Carlos Santos (MKT002)</div>
                                <div class="text-sm text-gray-600">📈 Marketing - 2,847 pts</div>
                            </div>
                            <div class="bg-purple-50 p-3 rounded-lg cursor-pointer hover:bg-purple-100 employee-option" onclick="selectEmployee(this, 'Maria Oliveira', 'TEC003')">
                                <div class="font-medium">Maria Oliveira (TEC003)</div>
                                <div class="text-sm text-gray-600">💻 Tecnologia - 2,654 pts</div>
                            </div>
                            <div class="bg-yellow-50 p-3 rounded-lg cursor-pointer hover:bg-yellow-100 employee-option" onclick="selectEmployee(this, 'João Costa', 'RH004')">
                                <div class="font-medium">João Costa (RH004)</div>
                                <div class="text-sm text-gray-600">👥 RH - 2,341 pts</div>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Resumo da Atribuição -->
                <div class="bg-purple-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-purple-800 mb-4">📋 Resumo da Atribuição</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">📝 Tarefa Selecionada</label>
                            <div id="selectedTask" class="bg-white p-3 rounded-lg border">Nenhuma tarefa selecionada</div>
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">👤 Funcionário Selecionado</label>
                            <div id="selectedEmployee" class="bg-white p-3 rounded-lg border">Nenhum funcionário selecionado</div>
                        </div>
                    </div>
                    <div class="mt-4">
                        <label class="block text-sm font-medium text-gray-700 mb-2">📅 Prazo para Conclusão</label>
                        <input type="date" id="assignDeadline" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                    </div>
                    <div class="mt-4">
                        <label class="block text-sm font-medium text-gray-700 mb-2">💬 Observações</label>
                        <textarea id="assignNotes" rows="3" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Instruções adicionais para o funcionário"></textarea>
                    </div>
                </div>
                
                <div class="flex justify-end space-x-4 pt-4">
                    <button onclick="closeAssignModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ❌ Cancelar
                    </button>
                    <button onclick="assignTask()" class="bg-purple-500 hover:bg-purple-600 text-white px-6 py-2 rounded-lg transition-colors">
                        👥 Atribuir Tarefa
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal do Relatório -->
    <div id="reportModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-4xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">📊 Relatório Mensal - Dezembro 2024</h2>
                <button onclick="closeModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <!-- Resumo Geral -->
                <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                    <div class="bg-blue-50 p-4 rounded-lg text-center">
                        <div class="text-2xl font-bold text-blue-600">150</div>
                        <div class="text-sm text-blue-600">Meta Mensal</div>
                    </div>
                    <div class="bg-green-50 p-4 rounded-lg text-center">
                        <div class="text-2xl font-bold text-green-600">127</div>
                        <div class="text-sm text-green-600">Concluídas</div>
                    </div>
                    <div class="bg-yellow-50 p-4 rounded-lg text-center">
                        <div class="text-2xl font-bold text-yellow-600">15</div>
                        <div class="text-sm text-yellow-600">Em Andamento</div>
                    </div>
                    <div class="bg-red-50 p-4 rounded-lg text-center">
                        <div class="text-2xl font-bold text-red-600">8</div>
                        <div class="text-sm text-red-600">Atrasadas</div>
                    </div>
                </div>

                <!-- Desempenho por Departamento -->
                <div class="bg-gray-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-gray-800 mb-4">📈 Desempenho por Departamento</h3>
                    <div class="space-y-4">
                        <div class="flex items-center justify-between">
                            <span class="font-medium">💰 Financeiro</span>
                            <div class="flex items-center space-x-2">
                                <div class="w-32 bg-gray-200 rounded-full h-3">
                                    <div class="bg-blue-500 h-3 rounded-full" style="width: 92%"></div>
                                </div>
                                <span class="text-sm font-bold text-blue-600">92%</span>
                            </div>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="font-medium">📈 Marketing</span>
                            <div class="flex items-center space-x-2">
                                <div class="w-32 bg-gray-200 rounded-full h-3">
                                    <div class="bg-green-500 h-3 rounded-full" style="width: 88%"></div>
                                </div>
                                <span class="text-sm font-bold text-green-600">88%</span>
                            </div>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="font-medium">💻 Tecnologia</span>
                            <div class="flex items-center space-x-2">
                                <div class="w-32 bg-gray-200 rounded-full h-3">
                                    <div class="bg-purple-500 h-3 rounded-full" style="width: 85%"></div>
                                </div>
                                <span class="text-sm font-bold text-purple-600">85%</span>
                            </div>
                        </div>
                        <div class="flex items-center justify-between">
                            <span class="font-medium">👥 Recursos Humanos</span>
                            <div class="flex items-center space-x-2">
                                <div class="w-32 bg-gray-200 rounded-full h-3">
                                    <div class="bg-yellow-500 h-3 rounded-full" style="width: 78%"></div>
                                </div>
                                <span class="text-sm font-bold text-yellow-600">78%</span>
                            </div>
                        </div>
                    </div>
                </div>

                <!-- Tarefas por Prioridade -->
                <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <div class="bg-red-50 p-4 rounded-lg">
                        <h4 class="font-semibold text-red-700 mb-2">😰 Urgentes</h4>
                        <div class="text-2xl font-bold text-red-600">23</div>
                        <div class="text-sm text-red-600">Concluídas: 19 (82.6%)</div>
                    </div>
                    <div class="bg-yellow-50 p-4 rounded-lg">
                        <h4 class="font-semibold text-yellow-700 mb-2">😐 Importantes</h4>
                        <div class="text-2xl font-bold text-yellow-600">67</div>
                        <div class="text-sm text-yellow-600">Concluídas: 58 (86.6%)</div>
                    </div>
                    <div class="bg-green-50 p-4 rounded-lg">
                        <h4 class="font-semibold text-green-700 mb-2">😊 Normais</h4>
                        <div class="text-2xl font-bold text-green-600">60</div>
                        <div class="text-sm text-green-600">Concluídas: 50 (83.3%)</div>
                    </div>
                </div>

                <!-- Botões de Ação -->
                <div class="flex justify-center space-x-4 pt-4">
                    <button onclick="exportReport()" class="bg-green-500 hover:bg-green-600 text-white px-6 py-2 rounded-lg transition-colors">
                        📄 Exportar PDF
                    </button>
                    <button onclick="shareReport()" class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-2 rounded-lg transition-colors">
                        📤 Compartilhar
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Adicionar Colaborador -->
    <div id="employeeModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-2xl w-full mx-4 max-h-[90vh] overflow-auto">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-2xl font-bold text-gray-800">👤 Adicionar Novo Colaborador</h2>
                <button onclick="closeEmployeeModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-6">
                <!-- Informações Básicas -->
                <div class="bg-blue-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-blue-800 mb-4">📋 Informações Básicas</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">👤 Nome Completo</label>
                            <input type="text" id="newEmployeeName" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="Digite o nome completo">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">📧 Email</label>
                            <input type="email" id="newEmployeeEmail" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="email@empresa.com">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">📱 Telefone</label>
                            <input type="tel" id="newEmployeePhone" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent" placeholder="(11) 99999-9999">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">🏢 Departamento</label>
                            <select id="newEmployeeDepartment" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent">
                                <option value="">Selecione o departamento</option>
                                <option value="Financeiro">💰 Financeiro</option>
                                <option value="Marketing">📈 Marketing</option>
                                <option value="Tecnologia">💻 Tecnologia</option>
                                <option value="Recursos Humanos">👥 Recursos Humanos</option>
                                <option value="Administrativo">📋 Administrativo</option>
                                <option value="Vendas">🏪 Vendas</option>
                            </select>
                        </div>
                    </div>
                </div>

                <!-- Informações de Acesso -->
                <div class="bg-green-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-green-800 mb-4">🔐 Informações de Acesso</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">🆔 ID do Colaborador</label>
                            <input type="text" id="newEmployeeId" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="Ex: FIN007, MKT008">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">🔒 Senha Inicial</label>
                            <input type="password" id="newEmployeePassword" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-green-500 focus:border-transparent" placeholder="Senha temporária">
                        </div>
                    </div>
                    <div class="mt-4">
                        <label class="flex items-center">
                            <input type="checkbox" id="sendWelcomeEmail" class="w-4 h-4 text-green-600 rounded" checked>
                            <span class="ml-2 text-sm text-gray-700">📧 Enviar email de boas-vindas com credenciais</span>
                        </label>
                    </div>
                </div>

                <!-- Informações Adicionais -->
                <div class="bg-purple-50 p-6 rounded-xl">
                    <h3 class="text-lg font-semibold text-purple-800 mb-4">⚙️ Configurações Adicionais</h3>
                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">👔 Cargo</label>
                            <input type="text" id="newEmployeePosition" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent" placeholder="Ex: Analista, Gerente">
                        </div>
                        <div>
                            <label class="block text-sm font-medium text-gray-700 mb-2">📅 Data de Admissão</label>
                            <input type="date" id="newEmployeeStartDate" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                        </div>
                    </div>
                    <div class="mt-4">
                        <label class="block text-sm font-medium text-gray-700 mb-2">👤 Perfil de Acesso</label>
                        <select id="newEmployeeRole" class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-purple-500 focus:border-transparent">
                            <option value="employee">👤 Funcionário</option>
                            <option value="manager">👨‍💼 Gestor</option>
                            <option value="admin">🔧 Administrador</option>
                        </select>
                    </div>
                </div>
                
                <div class="flex justify-end space-x-4 pt-4">
                    <button onclick="closeEmployeeModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-6 py-2 rounded-lg transition-colors">
                        ❌ Cancelar
                    </button>
                    <button onclick="saveEmployee()" class="bg-blue-500 hover:bg-blue-600 text-white px-6 py-2 rounded-lg transition-colors">
                        👤 Criar Colaborador
                    </button>
                </div>
            </div>
        </div>
    </div>

    <!-- Modal de Recuperação de Senha -->
    <div id="forgotPasswordModal" class="fixed inset-0 bg-black bg-opacity-50 hidden flex items-center justify-center z-50">
        <div class="bg-white rounded-2xl shadow-2xl max-w-md w-full mx-4">
            <div class="p-6 border-b border-gray-200 flex justify-between items-center">
                <h2 class="text-xl font-bold text-gray-800">🔑 Recuperar Senha</h2>
                <button onclick="closeForgotPasswordModal()" class="text-gray-500 hover:text-gray-700 text-2xl">✕</button>
            </div>
            
            <div class="p-6 space-y-4">
                <p class="text-gray-600 text-sm">Digite seu ID de funcionário para receber instruções de recuperação de senha.</p>
                
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-2">👤 ID do Funcionário</label>
                    <input 
                        type="text" 
                        id="recoveryEmployeeId" 
                        placeholder="Ex: FIN001, MKT002..."
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent"
                    >
                </div>
                
                <div class="flex justify-end space-x-3 pt-4">
                    <button onclick="closeForgotPasswordModal()" class="bg-gray-500 hover:bg-gray-600 text-white px-4 py-2 rounded-lg transition-colors">
                        ❌ Cancelar
                    </button>
                    <button onclick="sendRecoveryEmail()" class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg transition-colors">
                        📧 Enviar Instruções
                    </button>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Variáveis globais para gestão
        let selectedTaskForAssign = null;
        let selectedEmployeeForAssign = null;
        let customDepartments = [];
        let currentSelectedMonth = '2024-12';

        // ===== SISTEMA DE PERSISTÊNCIA DE DADOS =====
        
        // Função para carregar dados do localStorage
        function loadStoredData() {
            const storedEmployees = localStorage.getItem('gamificagestao_employees');
            const storedPasswords = localStorage.getItem('gamificagestao_passwords');
            const storedDepartments = localStorage.getItem('gamificagestao_departments');
            
            if (storedEmployees) {
                Object.assign(employees, JSON.parse(storedEmployees));
            }
            
            if (storedPasswords) {
                Object.assign(employeePasswords, JSON.parse(storedPasswords));
            }
            
            if (storedDepartments) {
                customDepartments = JSON.parse(storedDepartments);
                updateDepartmentSelects();
            }
        }

        // Função para salvar dados no localStorage
        function saveStoredData() {
            localStorage.setItem('gamificagestao_employees', JSON.stringify(employees));
            localStorage.setItem('gamificagestao_passwords', JSON.stringify(employeePasswords));
            localStorage.setItem('gamificagestao_departments', JSON.stringify(customDepartments));
        }

        // Sistema de senhas dos colaboradores
        let employeePasswords = {
            'FIN001': '123456',
            'MKT002': '123456',
            'TEC003': '123456',
            'RH004': '123456',
            'ADM005': '123456',
            'VEN006': '123456'
        };

        // Base de dados dos colaboradores (dados iniciais)
        const employees = {
            'FIN001': {
                name: 'Ana Silva',
                department: 'Financeiro',
                departmentIcon: '💰',
                score: 3250,
                ranking: '#1 da equipe',
                streak: 12,
                email: 'ana.silva@empresa.com',
                phone: '(11) 99999-0001',
                position: 'Gerente Financeiro',
                role: 'manager',
                profilePic: null
            },
            'MKT002': {
                name: 'Carlos Santos',
                department: 'Marketing',
                departmentIcon: '📈',
                score: 2847,
                ranking: '#2 da equipe',
                streak: 8,
                email: 'carlos.santos@empresa.com',
                phone: '(11) 99999-0002',
                position: 'Analista de Marketing',
                role: 'employee',
                profilePic: null
            },
            'TEC003': {
                name: 'Maria Oliveira',
                department: 'Tecnologia',
                departmentIcon: '💻',
                score: 2654,
                ranking: '#3 da equipe',
                streak: 7,
                email: 'maria.oliveira@empresa.com',
                phone: '(11) 99999-0003',
                position: 'Desenvolvedora Senior',
                role: 'employee',
                profilePic: null
            },
            'RH004': {
                name: 'João Costa',
                department: 'Recursos Humanos',
                departmentIcon: '👥',
                score: 2341,
                ranking: '#4 da equipe',
                streak: 5,
                email: 'joao.costa@empresa.com',
                phone: '(11) 99999-0004',
                position: 'Analista de RH',
                role: 'employee',
                profilePic: null
            },
            'ADM005': {
                name: 'Lucia Ferreira',
                department: 'Administrativo',
                departmentIcon: '📋',
                score: 2156,
                ranking: '#5 da equipe',
                streak: 4,
                email: 'lucia.ferreira@empresa.com',
                phone: '(11) 99999-0005',
                position: 'Assistente Administrativo',
                role: 'employee',
                profilePic: null
            },
            'VEN006': {
                name: 'Pedro Almeida',
                department: 'Vendas',
                departmentIcon: '🏪',
                score: 1987,
                ranking: '#6 da equipe',
                streak: 3,
                email: 'pedro.almeida@empresa.com',
                phone: '(11) 99999-0006',
                position: 'Consultor de Vendas',
                role: 'employee',
                profilePic: null
            }
        };

        // Tarefas mensais por departamento
        const monthlyTasksByDepartment = {
            'Financeiro': [
                { name: 'Relatório Financeiro Q4', priority: 'urgent', deadline: '15/12', status: 'pending' },
                { name: 'Auditoria Interna', priority: 'normal', deadline: '22/12', status: 'progress', progress: 65 },
                { name: 'Análise de Custos', priority: 'important', deadline: '25/12', status: 'pending' },
                { name: 'Aprovação Orçamento 2025', priority: 'urgent', deadline: '28/12', status: 'pending' }
            ],
            'Administrativo': [
                { name: 'Renovação Contratos', priority: 'important', deadline: '18/12', status: 'pending' },
                { name: 'Organização Arquivo', priority: 'normal', deadline: '24/12', status: 'pending' },
                { name: 'Compra Suprimentos', priority: 'important', deadline: '26/12', status: 'progress', progress: 40 },
                { name: 'Atualização Políticas', priority: 'normal', deadline: '30/12', status: 'pending' }
            ],
            'Marketing': [
                { name: 'Campanha Black Friday', priority: 'important', deadline: '18/12', status: 'pending' },
                { name: 'Criação de Conteúdo', priority: 'normal', deadline: '28/12', status: 'pending' },
                { name: 'Análise de Métricas', priority: 'important', deadline: '24/12', status: 'progress', progress: 55 },
                { name: 'Lançamento Produto', priority: 'urgent', deadline: '20/12', status: 'pending' }
            ],
            'Recursos Humanos': [
                { name: 'Processo Seletivo', priority: 'important', deadline: '20/12', status: 'pending' },
                { name: 'Treinamento Equipe', priority: 'normal', deadline: '29/12', status: 'pending' },
                { name: 'Avaliação Performance', priority: 'important', deadline: '26/12', status: 'progress', progress: 30 },
                { name: 'Onboarding Novatos', priority: 'normal', deadline: '31/12', status: 'pending' }
            ],
            'Tecnologia': [
                { name: 'Correção Bug Crítico', priority: 'urgent', deadline: '16/12', status: 'pending' },
                { name: 'Backup Servidores', priority: 'normal', deadline: '30/12', status: 'pending' },
                { name: 'Deploy Nova Versão', priority: 'important', deadline: '22/12', status: 'progress', progress: 75 },
                { name: 'Atualização Sistema', priority: 'important', deadline: '27/12', status: 'pending' }
            ],
            'Vendas': [
                { name: 'Prospecção Clientes', priority: 'important', deadline: '19/12', status: 'pending' },
                { name: 'Follow-up Propostas', priority: 'urgent', deadline: '16/12', status: 'pending' },
                { name: 'Relatório Vendas', priority: 'normal', deadline: '30/12', status: 'pending' },
                { name: 'Negociação Contrato', priority: 'urgent', deadline: '21/12', status: 'progress', progress: 80 }
            ]
        };

        // Tarefas por departamento
        const departmentTasks = {
            'Financeiro': {
                pending: [
                    { name: 'Aprovação Orçamento 2025', priority: 'urgent', deadline: '15/12' },
                    { name: 'Análise de Custos', priority: 'important', deadline: '23/12' },
                    { name: 'Auditoria Interna', priority: 'low', deadline: '29/12' }
                ],
                progress: [
                    { name: 'Relatório Financeiro Q4', priority: 'urgent', progress: 65 },
                    { name: 'Fechamento Contábil', priority: 'important', progress: 40 }
                ],
                completed: [
                    { name: 'Fechamento Mensal', priority: 'important', time: '14:30' },
                    { name: 'Pagamento Fornecedores', priority: 'low', time: '16:45' }
                ]
            },
            'Administrativo': {
                pending: [
                    { name: 'Renovação Contratos', priority: 'important', deadline: '20/12' },
                    { name: 'Organização Arquivo', priority: 'low', deadline: '28/12' },
                    { name: 'Compra Suprimentos', priority: 'important', deadline: '22/12' }
                ],
                progress: [
                    { name: 'Atualização Políticas', priority: 'important', progress: 60 },
                    { name: 'Inventário Patrimônio', priority: 'low', progress: 30 }
                ],
                completed: [
                    { name: 'Protocolo Documentos', priority: 'low', time: '11:20' },
                    { name: 'Reunião Diretoria', priority: 'important', time: '15:00' }
                ]
            },
            'Marketing': {
                pending: [
                    { name: 'Campanha Black Friday', priority: 'important', deadline: '18/12' },
                    { name: 'Criação de Conteúdo', priority: 'low', deadline: '28/12' },
                    { name: 'Análise de Métricas', priority: 'important', deadline: '24/12' }
                ],
                progress: [
                    { name: 'Lançamento Produto', priority: 'urgent', progress: 45 },
                    { name: 'Pesquisa de Mercado', priority: 'important', progress: 70 }
                ],
                completed: [
                    { name: 'Post Redes Sociais', priority: 'low', time: '10:15' },
                    { name: 'Reunião com Agência', priority: 'important', time: '15:20' }
                ]
            },
            'Recursos Humanos': {
                pending: [
                    { name: 'Processo Seletivo', priority: 'important', deadline: '23/12' },
                    { name: 'Treinamento Equipe', priority: 'low', deadline: '29/12' },
                    { name: 'Avaliação Performance', priority: 'important', deadline: '26/12' }
                ],
                progress: [
                    { name: 'Onboarding Novatos', priority: 'important', progress: 40 },
                    { name: 'Atualização Políticas RH', priority: 'low', progress: 75 }
                ],
                completed: [
                    { name: 'Reunião 1:1', priority: 'important', time: '11:00' },
                    { name: 'Folha de Pagamento', priority: 'low', time: '16:30' }
                ]
            },
            'Tecnologia': {
                pending: [
                    { name: 'Correção Bug Crítico', priority: 'urgent', deadline: '14/12' },
                    { name: 'Atualização Sistema', priority: 'important', deadline: '21/12' },
                    { name: 'Backup Servidores', priority: 'low', deadline: '31/12' }
                ],
                progress: [
                    { name: 'Deploy Nova Versão', priority: 'important', progress: 55 },
                    { name: 'Documentação API', priority: 'low', progress: 85 }
                ],
                completed: [
                    { name: 'Hotfix Produção', priority: 'urgent', time: '09:30' },
                    { name: 'Monitoramento Sistemas', priority: 'low', time: '17:00' }
                ]
            },
            'Vendas': {
                pending: [
                    { name: 'Prospecção Clientes', priority: 'important', deadline: '19/12' },
                    { name: 'Follow-up Propostas', priority: 'urgent', deadline: '16/12' },
                    { name: 'Relatório Vendas', priority: 'low', deadline: '30/12' }
                ],
                progress: [
                    { name: 'Negociação Contrato', priority: 'urgent', progress: 80 },
                    { name: 'Apresentação Cliente', priority: 'important', progress: 50 }
                ],
                completed: [
                    { name: 'Fechamento Venda', priority: 'important', time: '13:45' },
                    { name: 'Atualização CRM', priority: 'low', time: '16:20' }
                ]
            }
        };

        let currentDepartment = 'Financeiro'; // Departamento ativo atual

        let currentUser = null;

        // Dados históricos por mês
        const monthlyData = {
            '2024-12': {
                name: 'Dezembro 2024',
                emoji: '🎄',
                goal: 150,
                completed: 127,
                successRate: '84.7%'
            },
            '2024-11': {
                name: 'Novembro 2024',
                emoji: '🍂',
                goal: 145,
                completed: 138,
                successRate: '95.2%'
            },
            '2024-10': {
                name: 'Outubro 2024',
                emoji: '🎃',
                goal: 140,
                completed: 132,
                successRate: '94.3%'
            },
            '2024-09': {
                name: 'Setembro 2024',
                emoji: '🍁',
                goal: 135,
                completed: 128,
                successRate: '94.8%'
            },
            '2024-08': {
                name: 'Agosto 2024',
                emoji: '☀️',
                goal: 130,
                completed: 115,
                successRate: '88.5%'
            },
            '2024-07': {
                name: 'Julho 2024',
                emoji: '🏖️',
                goal: 125,
                completed: 118,
                successRate: '94.4%'
            },
            '2024-06': {
                name: 'Junho 2024',
                emoji: '🌻',
                goal: 120,
                completed: 112,
                successRate: '93.3%'
            },
            '2024-05': {
                name: 'Maio 2024',
                emoji: '🌸',
                goal: 115,
                completed: 108,
                successRate: '93.9%'
            },
            '2024-04': {
                name: 'Abril 2024',
                emoji: '🌷',
                goal: 110,
                completed: 98,
                successRate: '89.1%'
            },
            '2024-03': {
                name: 'Março 2024',
                emoji: '🌱',
                goal: 105,
                completed: 102,
                successRate: '97.1%'
            },
            '2024-02': {
                name: 'Fevereiro 2024',
                emoji: '💝',
                goal: 100,
                completed: 95,
                successRate: '95.0%'
            },
            '2024-01': {
                name: 'Janeiro 2024',
                emoji: '🎊',
                goal: 95,
                completed: 88,
                successRate: '92.6%'
            }
        };

        // Função para mudar o mês selecionado
        function changeMonth() {
            const monthSelector = document.getElementById('monthSelector');
            currentSelectedMonth = monthSelector.value;
            
            const monthData = monthlyData[currentSelectedMonth];
            
            // Atualiza o nome do mês no botão
            document.getElementById('selectedMonthName').textContent = monthData.name.split(' ')[0];
            
            // Atualiza o título das tarefas mensais
            document.getElementById('currentMonthTitle').textContent = monthData.name;
            
            // Atualiza as estatísticas do painel lateral
            document.getElementById('monthlyGoal').textContent = `${monthData.goal} tarefas`;
            document.getElementById('monthlyCompleted').textContent = `${monthData.completed} tarefas`;
            document.getElementById('successRate').textContent = monthData.successRate;
            
            // Simula carregamento de tarefas do mês selecionado
            loadMonthlyTasksForSelectedMonth();
            
            // Feedback visual
            const button = document.querySelector('button[onclick="generateMonthlyReport()"]');
            const originalText = button.innerHTML;
            button.innerHTML = `⏳ Carregando ${monthData.name.split(' ')[0]}...`;
            button.disabled = true;
            
            setTimeout(() => {
                button.innerHTML = originalText;
                button.disabled = false;
            }, 1000);
        }

        // Carrega tarefas do mês selecionado
        function loadMonthlyTasksForSelectedMonth() {
            const monthData = monthlyData[currentSelectedMonth];
            const container = document.getElementById('monthlyTasks');
            
            // Simula diferentes tarefas para cada mês
            const sampleTasks = generateSampleTasksForMonth(currentSelectedMonth);
            
            container.innerHTML = '';
            
            if (sampleTasks.length === 0) {
                container.innerHTML = '<div class="col-span-full text-center text-gray-500 py-8">Nenhuma tarefa para este mês</div>';
                return;
            }
            
            sampleTasks.forEach(task => {
                const taskElement = createMonthlyTaskElement(task);
                container.appendChild(taskElement);
            });
        }

        // Gera tarefas de exemplo para o mês selecionado
        function generateSampleTasksForMonth(monthKey) {
            const monthData = monthlyData[monthKey];
            const isCurrentMonth = monthKey === '2024-12';
            
            if (isCurrentMonth) {
                // Para dezembro, usa as tarefas normais
                return monthlyTasksByDepartment[currentDepartment] || [];
            }
            
            // Para meses anteriores, gera tarefas históricas
            const historicalTasks = [
                { name: `Relatório ${monthData.name}`, priority: 'important', deadline: '30/' + monthKey.split('-')[1], status: 'completed' },
                { name: `Fechamento ${monthData.name}`, priority: 'urgent', deadline: '28/' + monthKey.split('-')[1], status: 'completed' },
                { name: `Análise Mensal ${monthData.emoji}`, priority: 'normal', deadline: '25/' + monthKey.split('-')[1], status: 'completed' },
                { name: `Planejamento Seguinte`, priority: 'important', deadline: '31/' + monthKey.split('-')[1], status: 'completed' }
            ];
            
            return historicalTasks;
        }

        // Função de login
        function handleLogin(event) {
            event.preventDefault();
            
            const employeeId = document.getElementById('employeeId').value.toUpperCase();
            const password = document.getElementById('password').value;
            
            // Carrega dados salvos antes de validar
            loadStoredData();
            
            // Validação com senha armazenada
            if (employees[employeeId] && employeePasswords[employeeId] === password) {
                currentUser = employees[employeeId];
                currentUser.id = employeeId;
                
                // Esconde tela de login e mostra seleção de departamentos
                document.getElementById('loginScreen').classList.add('hidden');
                document.getElementById('departmentSelectionScreen').classList.remove('hidden');
                
                // Personaliza a tela de seleção
                document.getElementById('welcomeUserName').textContent = currentUser.name;
                
            } else {
                alert('❌ ID ou senha incorretos! Tente: FIN001, MKT002, TEC003, RH004 com senha 123456');
            }
        }

        // Personaliza o painel para o usuário logado
        function personalizePanel() {
            document.getElementById('userName').textContent = currentUser.name;
            document.getElementById('userDepartment').textContent = `${getDepartmentIcon(currentDepartment)} ${currentDepartment}`;
            document.getElementById('userScore').textContent = `${currentUser.score.toLocaleString()} pts`;
            document.getElementById('userRanking').textContent = currentUser.ranking;
            document.getElementById('currentStreak').textContent = `${currentUser.streak} dias`;
            
            // Controla visibilidade da seção de gestão (apenas para gestores)
            const managementSection = document.getElementById('managementSection');
            if (currentUser.id === 'FIN001' || currentUser.id === 'MKT002') {
                managementSection.style.display = 'block';
            } else {
                managementSection.style.display = 'none';
            }
            
            // Carrega preferência do painel lateral
            const savedSidebarState = localStorage.getItem('gamificagestao_sidebar_visible');
            if (savedSidebarState !== null) {
                sidebarVisible = savedSidebarState === 'true';
                if (!sidebarVisible) {
                    // Aplica estado fechado sem animação na inicialização
                    const sidebar = document.getElementById('sidebar');
                    const mainContent = document.getElementById('mainContent');
                    const toggleIcon = document.getElementById('toggleIcon');
                    
                    sidebar.classList.add('-translate-x-full');
                    sidebar.classList.remove('translate-x-0');
                    mainContent.style.marginLeft = '0';
                    toggleIcon.textContent = '📋';
                    document.getElementById('toggleSidebar').title = 'Abrir Painel de Controle';
                }
            }
            
            // Inicia atualizações em tempo real
            startRealTimeUpdates();
            
            // Atualiza lista de usuários online imediatamente
            updateOnlineUsers();
        }

        // Função removida - não há mais abas de departamento no painel principal

        // Carrega tarefas mensais do departamento selecionado
        function loadMonthlyTasks(department = null) {
            const targetDept = department || currentDepartment;
            const monthlyTasks = monthlyTasksByDepartment[targetDept];
            const container = document.getElementById('monthlyTasks');
            
            container.innerHTML = '';
            
            if (!monthlyTasks || monthlyTasks.length === 0) {
                container.innerHTML = '<div class="col-span-full text-center text-gray-500 py-8">Nenhuma tarefa mensal para este departamento</div>';
                return;
            }
            
            monthlyTasks.forEach(task => {
                const taskElement = createMonthlyTaskElement(task);
                container.appendChild(taskElement);
            });
        }

        // Cria elemento de tarefa mensal
        function createMonthlyTaskElement(task) {
            const div = document.createElement('div');
            const priorityEmoji = task.priority === 'urgent' ? '😰' : task.priority === 'important' ? '😐' : '😊';
            const priorityText = task.priority === 'urgent' ? 'URGENTE' : task.priority === 'important' ? 'IMPORTANTE' : 'NORMAL';
            const priorityColor = task.priority === 'urgent' ? 'red' : task.priority === 'important' ? 'yellow' : 'green';
            const statusText = task.status === 'progress' ? 'EM PROGRESSO' : task.status === 'completed' ? 'CONCLUÍDA' : priorityText;
            const statusColor = task.status === 'progress' ? 'blue' : task.status === 'completed' ? 'green' : priorityColor;
            const statusEmoji = task.status === 'progress' ? '🔄' : task.status === 'completed' ? '✅' : priorityEmoji;
            
            div.className = `bg-${statusColor}-50 p-4 rounded-xl border-l-4 border-${statusColor}-500 task-card`;
            
            let content = `
                <div class="flex items-center justify-between mb-2">
                    <span class="text-sm font-semibold text-${statusColor}-700">${statusEmoji} ${statusText}</span>
                    <span class="text-xs bg-${statusColor}-100 text-${statusColor}-800 px-2 py-1 rounded-full">${task.deadline}</span>
                </div>
                <h3 class="font-medium text-gray-800 mb-1">${task.name}</h3>
                <p class="text-xs text-gray-600 mb-2">${getDepartmentIcon(currentDepartment)} ${currentDepartment}</p>
            `;
            
            if (task.status === 'progress' && task.progress) {
                content += `
                    <div class="mb-2">
                        <div class="bg-gray-200 rounded-full h-2">
                            <div class="bg-${statusColor}-500 h-2 rounded-full" style="width: ${task.progress}%"></div>
                        </div>
                        <span class="text-xs text-${statusColor}-600">${task.progress}% concluído</span>
                    </div>
                `;
            }
            
            if (task.status === 'completed') {
                content += `<button class="bg-gray-400 text-white px-2 py-1 rounded text-xs cursor-not-allowed" disabled>✅ Concluída</button>`;
            } else if (task.status === 'progress') {
                content += `<button onclick="moveTaskFromMonthly(this, 'completed')" class="bg-${statusColor}-500 hover:bg-${statusColor}-600 text-white px-2 py-1 rounded text-xs">Continuar</button>`;
            } else {
                content += `<button onclick="moveTaskFromMonthly(this, 'progress')" class="bg-${priorityColor}-500 hover:bg-${priorityColor}-600 text-white px-2 py-1 rounded text-xs">Iniciar</button>`;
            }
            
            div.innerHTML = content;
            return div;
        }

        // Carrega tarefas do departamento selecionado
        function loadDepartmentTasks(department = null) {
            const targetDept = department || currentDepartment;
            const tasks = departmentTasks[targetDept];
            
            // Carrega também as tarefas mensais
            loadMonthlyTasks(targetDept);
            
            // Se não existir tarefas para o departamento, cria estrutura vazia
            if (!tasks) {
                const pendingContainer = document.getElementById('pendingTasks');
                const progressContainer = document.getElementById('progressTasks');
                const completedContainer = document.getElementById('completedTasks');
                
                pendingContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa pendente</div>';
                progressContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa em andamento</div>';
                completedContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa concluída</div>';
                
                updateCounters();
                return;
            }
            
            // Carrega tarefas pendentes
            const pendingContainer = document.getElementById('pendingTasks');
            pendingContainer.innerHTML = '';
            if (tasks.pending && tasks.pending.length > 0) {
                tasks.pending.forEach(task => {
                    const taskElement = createTaskElement(task, 'pending');
                    pendingContainer.appendChild(taskElement);
                });
            } else {
                pendingContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa pendente</div>';
            }
            
            // Carrega tarefas em progresso
            const progressContainer = document.getElementById('progressTasks');
            progressContainer.innerHTML = '';
            if (tasks.progress && tasks.progress.length > 0) {
                tasks.progress.forEach(task => {
                    const taskElement = createTaskElement(task, 'progress');
                    progressContainer.appendChild(taskElement);
                });
            } else {
                progressContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa em andamento</div>';
            }
            
            // Carrega tarefas concluídas
            const completedContainer = document.getElementById('completedTasks');
            completedContainer.innerHTML = '';
            if (tasks.completed && tasks.completed.length > 0) {
                tasks.completed.forEach(task => {
                    const taskElement = createTaskElement(task, 'completed');
                    completedContainer.appendChild(taskElement);
                });
            } else {
                completedContainer.innerHTML = '<div class="text-center text-gray-500 py-4">Nenhuma tarefa concluída</div>';
            }
            
            // Atualiza contadores
            updateCounters();
        }

        // Cria elemento de tarefa
        function createTaskElement(task, status) {
            const div = document.createElement('div');
            const priorityEmoji = task.priority === 'urgent' ? '😰' : task.priority === 'important' ? '😐' : '😊';
            const priorityColor = task.priority === 'urgent' ? 'red' : task.priority === 'important' ? 'yellow' : 'green';
            const priorityText = task.priority === 'urgent' ? 'Urgente' : task.priority === 'important' ? 'Importante' : 'Normal';
            
            if (status === 'pending') {
                div.className = `bg-white p-4 rounded-lg shadow-sm border-l-4 border-${priorityColor}-500`;
                div.innerHTML = `
                    <div class="flex items-center justify-between">
                        <span class="font-medium">${task.name}</span>
                        <button onclick="moveTask(this, 'progress')" class="bg-yellow-500 hover:bg-yellow-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                            ▶️ Iniciar
                        </button>
                    </div>
                    <span class="text-xs text-gray-500">${priorityEmoji} ${priorityText} - Prazo: ${task.deadline}</span>
                `;
            } else if (status === 'progress') {
                div.className = `bg-white p-4 rounded-lg shadow-sm border-l-4 border-${priorityColor}-500`;
                div.innerHTML = `
                    <div class="flex items-center justify-between">
                        <span class="font-medium">${task.name}</span>
                        <button onclick="moveTask(this, 'completed')" class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                            ✅ Concluir
                        </button>
                    </div>
                    <div class="mt-2 bg-gray-200 rounded-full h-2">
                        <div class="bg-yellow-500 h-2 rounded-full" style="width: ${task.progress}%"></div>
                    </div>
                    <span class="text-xs text-gray-600">${task.progress}% concluído</span>
                `;
            } else if (status === 'completed') {
                div.className = `bg-white p-4 rounded-lg shadow-sm border-l-4 border-${priorityColor}-500 opacity-75`;
                div.innerHTML = `
                    <div class="flex items-center justify-between">
                        <span class="font-medium line-through">${task.name}</span>
                        <span class="text-green-600 font-bold">✅</span>
                    </div>
                    <span class="text-xs text-gray-500">🎉 Concluído às ${task.time}</span>
                `;
            }
            
            return div;
        }

        // Função para mover tarefas entre zonas
        function moveTask(button, targetZone) {
            const taskCard = button.closest('.bg-white');
            const taskName = taskCard.querySelector('span.font-medium').textContent;
            
            // Remove da zona atual
            taskCard.remove();
            
            // Atualiza contadores
            updateCounters();
            
            // Adiciona na zona de destino
            if (targetZone === 'progress') {
                addToProgress(taskName);
            } else if (targetZone === 'completed') {
                addToCompleted(taskName);
            }
            
            // Atualiza progresso
            updateDailyProgress();
        }

        // Função para mover tarefas do painel mensal
        function moveTaskFromMonthly(button, targetZone) {
            const taskCard = button.closest('.task-card');
            const taskName = taskCard.querySelector('h3').textContent;
            
            // Adiciona na zona de destino
            if (targetZone === 'progress') {
                addToProgress(taskName);
            } else if (targetZone === 'completed') {
                addToCompleted(taskName);
            }
            
            // Atualiza contadores e progresso
            updateCounters();
            updateDailyProgress();
            
            // Feedback visual
            button.innerHTML = '✅ Adicionada!';
            button.disabled = true;
            setTimeout(() => {
                button.innerHTML = targetZone === 'progress' ? 'Iniciar' : 'Continuar';
                button.disabled = false;
            }, 2000);
        }
        
        function addToProgress(taskName) {
            const progressZone = document.getElementById('progressTasks');
            const newTask = document.createElement('div');
            newTask.className = 'bg-white p-4 rounded-lg shadow-sm border-l-4 border-yellow-500';
            newTask.innerHTML = `
                <div class="flex items-center justify-between">
                    <span class="font-medium">${taskName}</span>
                    <button onclick="moveTask(this, 'completed')" class="bg-green-500 hover:bg-green-600 text-white px-3 py-1 rounded-full text-sm transition-colors">
                        ✅ Concluir
                    </button>
                </div>
                <div class="mt-2 bg-gray-200 rounded-full h-2">
                    <div class="bg-yellow-500 h-2 rounded-full" style="width: 30%"></div>
                </div>
                <span class="text-xs text-gray-600">30% concluído</span>
            `;
            progressZone.appendChild(newTask);
        }
        
        function addToCompleted(taskName) {
            const completedZone = document.getElementById('completedTasks');
            const newTask = document.createElement('div');
            newTask.className = 'bg-white p-4 rounded-lg shadow-sm border-l-4 border-green-500 opacity-75';
            const currentTime = new Date().toLocaleTimeString('pt-BR', {hour: '2-digit', minute: '2-digit'});
            newTask.innerHTML = `
                <div class="flex items-center justify-between">
                    <span class="font-medium line-through">${taskName}</span>
                    <span class="text-green-600 font-bold">✅</span>
                </div>
                <span class="text-xs text-gray-500">🎉 Concluído às ${currentTime}</span>
            `;
            completedZone.appendChild(newTask);
        }
        
        function updateCounters() {
            // Conta apenas elementos de tarefa reais (não mensagens de "nenhuma tarefa")
            const pendingTasks = document.querySelectorAll('#pendingTasks .bg-white');
            const progressTasks = document.querySelectorAll('#progressTasks .bg-white');
            const completedTasks = document.querySelectorAll('#completedTasks .bg-white');
            
            const pendingCount = pendingTasks.length;
            const progressCount = progressTasks.length;
            const completedCount = completedTasks.length;
            
            document.getElementById('pendingCount').textContent = pendingCount;
            document.getElementById('progressCount').textContent = progressCount;
            document.getElementById('completedCount').textContent = completedCount;
            document.getElementById('completedTotal').textContent = completedCount;
            
            // Atualiza títulos das zonas
            document.querySelector('.zone-pending h3').innerHTML = `😰 Pendentes (${pendingCount})`;
            document.querySelector('.zone-progress h3').innerHTML = `😐 Em Andamento (${progressCount})`;
            document.querySelector('.zone-completed h3').innerHTML = `😊 Concluídas (${completedCount})`;
        }
        
        function updateDailyProgress() {
            const totalTasks = 7; // Meta diária
            const completedTasks = document.querySelectorAll('#completedTasks .bg-white').length;
            const progressPercentage = (completedTasks / totalTasks * 100).toFixed(1);
            
            const progressBar = document.getElementById('dailyProgress');
            progressBar.style.width = progressPercentage + '%';
            progressBar.textContent = progressPercentage + '%';
        }
        
        // Função para trocar de departamento
        function switchDepartment(departmentName) {
            currentDepartment = departmentName;
            loadDepartmentTasks(departmentName);
        }

        // ===== INICIALIZAÇÃO DO SISTEMA =====
        
        // Inicializar sistema ao carregar a página
        document.addEventListener('DOMContentLoaded', function() {
            // Carrega dados salvos
            loadStoredData();
            
            // Sistema inicializado - sem necessidade de interatividade das abas

            // Adiciona botão para limpar dados (apenas para desenvolvimento/teste)
            if (window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1') {
                const resetButton = document.createElement('button');
                resetButton.innerHTML = '🔄 Resetar Sistema';
                resetButton.className = 'fixed bottom-4 right-4 bg-red-500 hover:bg-red-600 text-white px-4 py-2 rounded-lg text-sm z-50';
                resetButton.onclick = function() {
                    if (confirm('⚠️ Tem certeza que deseja resetar todos os dados do sistema?\n\nEsta ação não pode ser desfeita!')) {
                        localStorage.removeItem('gamificagestao_employees');
                        localStorage.removeItem('gamificagestao_passwords');
                        localStorage.removeItem('gamificagestao_departments');
                        alert('✅ Sistema resetado! Recarregue a página.');
                        location.reload();
                    }
                };
                document.body.appendChild(resetButton);
            }
        });

        // Função para selecionar departamento
        function selectDepartment(departmentName) {
            currentDepartment = departmentName;
            
            // Esconde tela de seleção e mostra painel principal
            document.getElementById('departmentSelectionScreen').classList.add('hidden');
            document.getElementById('mainPanel').classList.remove('hidden');
            
            // Personaliza o painel para o departamento selecionado
            personalizePanel();
            loadDepartmentTasks(departmentName);
            
            // Atualiza o título do departamento
            document.getElementById('currentDepartmentTitle').textContent = getDepartmentIcon(departmentName) + ' ' + departmentName;
            document.getElementById('departmentName').textContent = getDepartmentIcon(departmentName) + ' ' + departmentName;
        }

        // Função para voltar ao login
        function backToLogin() {
            document.getElementById('departmentSelectionScreen').classList.add('hidden');
            document.getElementById('loginScreen').classList.remove('hidden');
            
            // Limpa os campos de login
            document.getElementById('employeeId').value = '';
            document.getElementById('password').value = '';
            
            // Limpa dados do usuário atual
            currentUser = null;
        }

        // Função para voltar à seleção de departamentos
        function backToDepartmentSelection() {
            document.getElementById('mainPanel').classList.add('hidden');
            document.getElementById('departmentSelectionScreen').classList.remove('hidden');
            
            // Fecha todos os modais que possam estar abertos
            closeProfileModal();
            closeModal();
            closeTaskModal();
            closeDepartmentModal();
            closeAssignModal();
            closeEmployeeModal();
            closeForgotPasswordModal();
        }

        // Função de logout
        function logout() {
            if (confirm('🚪 Tem certeza que deseja sair?')) {
                // Esconde todos os painéis
                document.getElementById('mainPanel').classList.add('hidden');
                document.getElementById('departmentSelectionScreen').classList.add('hidden');
                
                // Mostra a tela de login
                document.getElementById('loginScreen').classList.remove('hidden');
                
                // Limpa os campos de login
                document.getElementById('employeeId').value = '';
                document.getElementById('password').value = '';
                
                // Limpa dados do usuário atual
                currentUser = null;
                
                // Fecha todos os modais que possam estar abertos
                closeProfileModal();
                closeModal();
                closeTaskModal();
                closeDepartmentModal();
                closeAssignModal();
                closeEmployeeModal();
                closeForgotPasswordModal();
                
                // Feedback visual de logout
                const loginCard = document.querySelector('.login-card');
                loginCard.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    loginCard.style.transform = 'scale(1)';
                }, 200);
                
                console.log('✅ Logout realizado com sucesso');
            }
        }

        // Funções do Relatório Mensal
        function generateMonthlyReport() {
            document.getElementById('reportModal').classList.remove('hidden');
        }

        function closeModal() {
            document.getElementById('reportModal').classList.add('hidden');
        }

        function exportReport() {
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '⏳ Gerando PDF...';
            button.disabled = true;
            
            setTimeout(() => {
                button.innerHTML = '✅ PDF Gerado!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                }, 2000);
            }, 2000);
        }

        function shareReport() {
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '📤 Compartilhando...';
            button.disabled = true;
            
            setTimeout(() => {
                button.innerHTML = '✅ Compartilhado!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                }, 2000);
            }, 2000);
        }

        // Funções do Modal de Perfil
        function openProfileModal() {
            // Preenche os campos com dados do usuário atual
            document.getElementById('profileName').value = currentUser.name;
            document.getElementById('profileEmail').value = currentUser.email || `${currentUser.id.toLowerCase()}@empresa.com`;
            document.getElementById('profilePhone').value = currentUser.phone || '';
            document.getElementById('profileDepartment').value = `${currentUser.departmentIcon} ${currentUser.department}`;
            
            // Mostra a foto atual se existir
            if (currentUser.profilePic) {
                document.getElementById('profilePicDisplay').innerHTML = `<img src="${currentUser.profilePic}" class="w-32 h-32 rounded-full object-cover">`;
                document.getElementById('profilePicPreview').innerHTML = `<img src="${currentUser.profilePic}" class="w-16 h-16 rounded-full object-cover">`;
            }
            
            document.getElementById('profileModal').classList.remove('hidden');
        }

        function closeProfileModal() {
            document.getElementById('profileModal').classList.add('hidden');
            // Limpa os campos de senha
            document.getElementById('currentPassword').value = '';
            document.getElementById('newPassword').value = '';
            document.getElementById('confirmPassword').value = '';
        }

        function handleProfilePicChange(event) {
            const file = event.target.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const imageUrl = e.target.result;
                    document.getElementById('profilePicDisplay').innerHTML = `<img src="${imageUrl}" class="w-32 h-32 rounded-full object-cover">`;
                    document.getElementById('profilePicPreview').innerHTML = `<img src="${imageUrl}" class="w-16 h-16 rounded-full object-cover">`;
                    
                    // Salva temporariamente
                    currentUser.profilePic = imageUrl;
                };
                reader.readAsDataURL(file);
            }
        }

        function removeProfilePic() {
            document.getElementById('profilePicDisplay').innerHTML = '👤';
            document.getElementById('profilePicPreview').innerHTML = '👤';
            currentUser.profilePic = null;
            document.getElementById('profilePicInput').value = '';
        }

        function saveProfile() {
            const newName = document.getElementById('profileName').value;
            const newEmail = document.getElementById('profileEmail').value;
            const newPhone = document.getElementById('profilePhone').value;
            const currentPassword = document.getElementById('currentPassword').value;
            const newPassword = document.getElementById('newPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;

            // Validações
            if (!newName.trim()) {
                alert('❌ Nome é obrigatório!');
                return;
            }

            if (!newEmail.trim()) {
                alert('❌ Email é obrigatório!');
                return;
            }

            // Validação de senha se preenchida
            if (currentPassword || newPassword || confirmPassword) {
                if (currentPassword !== employeePasswords[currentUser.id]) {
                    alert('❌ Senha atual incorreta!');
                    return;
                }
                
                if (newPassword.length < 6) {
                    alert('❌ Nova senha deve ter pelo menos 6 caracteres!');
                    return;
                }
                
                if (newPassword !== confirmPassword) {
                    alert('❌ Confirmação de senha não confere!');
                    return;
                }
                
                // Atualiza a senha
                employeePasswords[currentUser.id] = newPassword;
            }

            // Salva as alterações no objeto do usuário
            employees[currentUser.id].name = newName;
            employees[currentUser.id].email = newEmail;
            employees[currentUser.id].phone = newPhone;
            
            // Atualiza referência do currentUser
            currentUser.name = newName;
            currentUser.email = newEmail;
            currentUser.phone = newPhone;

            // Atualiza a interface
            document.getElementById('userName').textContent = currentUser.name;

            // Salva no localStorage
            saveStoredData();

            // Simula salvamento
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '⏳ Salvando...';
            button.disabled = true;

            setTimeout(() => {
                button.innerHTML = '✅ Salvo!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                    closeProfileModal();
                    alert('✅ Perfil atualizado com sucesso! As alterações foram salvas permanentemente.');
                }, 1000);
            }, 1500);
        }

        // ===== FUNÇÕES DE GESTÃO DE TAREFAS =====
        
        // Abrir modal de adicionar tarefa
        function openTaskModal() {
            document.getElementById('taskModal').classList.remove('hidden');
        }

        // Fechar modal de adicionar tarefa
        function closeTaskModal() {
            document.getElementById('taskModal').classList.add('hidden');
            // Limpar campos
            document.getElementById('taskName').value = '';
            document.getElementById('taskDepartment').value = '';
            document.getElementById('taskPriority').value = 'low';
            document.getElementById('taskDueDate').value = '';
            document.getElementById('taskDescription').value = '';
        }

        // Salvar nova tarefa
        function saveTask() {
            const name = document.getElementById('taskName').value;
            const department = document.getElementById('taskDepartment').value;
            const priority = document.getElementById('taskPriority').value;
            const dueDate = document.getElementById('taskDueDate').value;
            const description = document.getElementById('taskDescription').value;

            if (!name.trim()) {
                alert('❌ Nome da tarefa é obrigatório!');
                return;
            }

            if (!department) {
                alert('❌ Selecione um departamento!');
                return;
            }

            // Simula salvamento
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '⏳ Criando...';
            button.disabled = true;

            setTimeout(() => {
                button.innerHTML = '✅ Criada!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                    closeTaskModal();
                    alert(`✅ Tarefa "${name}" criada com sucesso para o departamento ${department}!`);
                }, 1000);
            }, 1500);
        }

        // ===== FUNÇÕES DE GESTÃO DE DEPARTAMENTOS =====
        
        // Abrir modal de departamentos
        function openDepartmentModal() {
            document.getElementById('departmentModal').classList.remove('hidden');
        }

        // Fechar modal de departamentos
        function closeDepartmentModal() {
            document.getElementById('departmentModal').classList.add('hidden');
            document.getElementById('newDeptName').value = '';
            document.getElementById('newDeptIcon').value = '';
        }

        // Função para atualizar selects de departamento
        function updateDepartmentSelects() {
            const taskDeptSelect = document.getElementById('taskDepartment');
            const employeeDeptSelect = document.getElementById('newEmployeeDepartment');
            
            // Adiciona departamentos customizados aos selects
            customDepartments.forEach(dept => {
                // Verifica se já existe antes de adicionar
                if (!Array.from(taskDeptSelect.options).some(option => option.value === dept.name)) {
                    const taskOption = document.createElement('option');
                    taskOption.value = dept.name;
                    taskOption.textContent = `${dept.icon} ${dept.name}`;
                    taskDeptSelect.appendChild(taskOption);
                }
                
                if (!Array.from(employeeDeptSelect.options).some(option => option.value === dept.name)) {
                    const employeeOption = document.createElement('option');
                    employeeOption.value = dept.name;
                    employeeOption.textContent = `${dept.icon} ${dept.name}`;
                    employeeDeptSelect.appendChild(employeeOption);
                }
            });
        }

        // Adicionar novo departamento
        function addDepartment() {
            const name = document.getElementById('newDeptName').value;
            const icon = document.getElementById('newDeptIcon').value;

            if (!name.trim()) {
                alert('❌ Nome do departamento é obrigatório!');
                return;
            }

            if (!icon.trim()) {
                alert('❌ Ícone do departamento é obrigatório!');
                return;
            }

            // Verifica se já existe
            if (customDepartments.some(dept => dept.name === name)) {
                alert('❌ Este departamento já existe!');
                return;
            }

            // Adiciona ao array de departamentos customizados
            customDepartments.push({ name: name, icon: icon });

            // Adiciona à lista visual
            const departmentsList = document.getElementById('departmentsList');
            const newDeptDiv = document.createElement('div');
            newDeptDiv.className = 'bg-indigo-50 p-4 rounded-lg flex items-center justify-between';
            newDeptDiv.innerHTML = `
                <span class="font-medium">${icon} ${name}</span>
                <div class="space-x-2">
                    <button onclick="editDepartment('${name}')" class="bg-blue-500 hover:bg-blue-600 text-white px-3 py-1 rounded text-sm">✏️ Editar</button>
                    <button onclick="deleteDepartment('${name}')" class="bg-red-500 hover:bg-red-600 text-white px-3 py-1 rounded text-sm">🗑️ Excluir</button>
                </div>
            `;
            departmentsList.appendChild(newDeptDiv);

            // Atualiza os selects
            updateDepartmentSelects();

            // Salva no localStorage
            saveStoredData();

            // Limpa campos
            document.getElementById('newDeptName').value = '';
            document.getElementById('newDeptIcon').value = '';

            alert(`✅ Departamento "${icon} ${name}" adicionado com sucesso e salvo permanentemente!`);
        }

        // Editar departamento
        function editDepartment(deptName) {
            const newName = prompt(`✏️ Novo nome para o departamento "${deptName}":`, deptName);
            if (newName && newName.trim() && newName !== deptName) {
                alert(`✅ Departamento "${deptName}" renomeado para "${newName}"!`);
            }
        }

        // Excluir departamento
        function deleteDepartment(deptName) {
            if (confirm(`🗑️ Tem certeza que deseja excluir o departamento "${deptName}"?\n\nEsta ação não pode ser desfeita.`)) {
                // Remove da lista visual
                const deptElements = document.querySelectorAll('#departmentsList > div');
                deptElements.forEach(element => {
                    if (element.textContent.includes(deptName)) {
                        element.remove();
                    }
                });
                alert(`✅ Departamento "${deptName}" excluído com sucesso!`);
            }
        }

        // ===== FUNÇÕES DE ATRIBUIÇÃO DE TAREFAS =====
        
        // Abrir modal de atribuição
        function openAssignModal() {
            document.getElementById('assignModal').classList.remove('hidden');
            resetAssignmentSelections();
        }

        // Fechar modal de atribuição
        function closeAssignModal() {
            document.getElementById('assignModal').classList.add('hidden');
            resetAssignmentSelections();
        }

        // Resetar seleções
        function resetAssignmentSelections() {
            selectedTaskForAssign = null;
            selectedEmployeeForAssign = null;
            document.getElementById('selectedTask').textContent = 'Nenhuma tarefa selecionada';
            document.getElementById('selectedEmployee').textContent = 'Nenhum funcionário selecionado';
            document.getElementById('assignDeadline').value = '';
            document.getElementById('assignNotes').value = '';
            
            // Remove seleções visuais
            document.querySelectorAll('.task-option').forEach(el => el.classList.remove('ring-2', 'ring-purple-500'));
            document.querySelectorAll('.employee-option').forEach(el => el.classList.remove('ring-2', 'ring-purple-500'));
        }

        // Selecionar tarefa
        function selectTask(element, taskName) {
            // Remove seleção anterior
            document.querySelectorAll('.task-option').forEach(el => el.classList.remove('ring-2', 'ring-purple-500'));
            
            // Adiciona seleção atual
            element.classList.add('ring-2', 'ring-purple-500');
            
            selectedTaskForAssign = taskName;
            document.getElementById('selectedTask').textContent = taskName;
        }

        // Selecionar funcionário
        function selectEmployee(element, employeeName, employeeId) {
            // Remove seleção anterior
            document.querySelectorAll('.employee-option').forEach(el => el.classList.remove('ring-2', 'ring-purple-500'));
            
            // Adiciona seleção atual
            element.classList.add('ring-2', 'ring-purple-500');
            
            selectedEmployeeForAssign = { name: employeeName, id: employeeId };
            document.getElementById('selectedEmployee').textContent = `${employeeName} (${employeeId})`;
        }

        // Atribuir tarefa
        function assignTask() {
            if (!selectedTaskForAssign) {
                alert('❌ Selecione uma tarefa!');
                return;
            }

            if (!selectedEmployeeForAssign) {
                alert('❌ Selecione um funcionário!');
                return;
            }

            const deadline = document.getElementById('assignDeadline').value;
            if (!deadline) {
                alert('❌ Defina um prazo para a tarefa!');
                return;
            }

            const notes = document.getElementById('assignNotes').value;

            // Simula atribuição
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '⏳ Atribuindo...';
            button.disabled = true;

            setTimeout(() => {
                button.innerHTML = '✅ Atribuída!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                    closeAssignModal();
                    alert(`✅ Tarefa "${selectedTaskForAssign}" atribuída com sucesso para ${selectedEmployeeForAssign.name}!\n\nPrazo: ${new Date(deadline).toLocaleDateString('pt-BR')}`);
                }, 1000);
            }, 1500);
        }

        // ===== FUNÇÕES DE RECUPERAÇÃO DE SENHA =====
        
        // Alternar visibilidade da senha
        function togglePassword() {
            const passwordField = document.getElementById('password');
            const eyeIcon = document.getElementById('eyeIcon');
            
            if (passwordField.type === 'password') {
                passwordField.type = 'text';
                eyeIcon.textContent = '🙈';
            } else {
                passwordField.type = 'password';
                eyeIcon.textContent = '👁️';
            }
        }

        // Abrir modal de recuperação de senha
        function openForgotPasswordModal() {
            document.getElementById('forgotPasswordModal').classList.remove('hidden');
        }

        // Fechar modal de recuperação de senha
        function closeForgotPasswordModal() {
            document.getElementById('forgotPasswordModal').classList.add('hidden');
            document.getElementById('recoveryEmployeeId').value = '';
        }

        // Enviar email de recuperação
        function sendRecoveryEmail() {
            const employeeId = document.getElementById('recoveryEmployeeId').value.toUpperCase();
            
            if (!employeeId.trim()) {
                alert('❌ Digite seu ID de funcionário!');
                return;
            }

            if (!employees[employeeId]) {
                alert('❌ ID de funcionário não encontrado!');
                return;
            }

            // Simula envio de email
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '📧 Enviando...';
            button.disabled = true;

            setTimeout(() => {
                button.innerHTML = '✅ Enviado!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                    closeForgotPasswordModal();
                    alert(`✅ Instruções de recuperação enviadas para o email cadastrado do funcionário ${employeeId}!\n\n📧 Verifique sua caixa de entrada e spam.`);
                }, 1000);
            }, 2000);
        }

        // ===== FUNÇÕES DE GESTÃO DE COLABORADORES =====
        
        // Abrir modal de adicionar colaborador
        function openEmployeeModal() {
            document.getElementById('employeeModal').classList.remove('hidden');
            // Define data atual como padrão
            document.getElementById('newEmployeeStartDate').value = new Date().toISOString().split('T')[0];
        }

        // Fechar modal de adicionar colaborador
        function closeEmployeeModal() {
            document.getElementById('employeeModal').classList.add('hidden');
            // Limpar todos os campos
            document.getElementById('newEmployeeName').value = '';
            document.getElementById('newEmployeeEmail').value = '';
            document.getElementById('newEmployeePhone').value = '';
            document.getElementById('newEmployeeDepartment').value = '';
            document.getElementById('newEmployeeId').value = '';
            document.getElementById('newEmployeePassword').value = '';
            document.getElementById('newEmployeePosition').value = '';
            document.getElementById('newEmployeeStartDate').value = '';
            document.getElementById('newEmployeeRole').value = 'employee';
            document.getElementById('sendWelcomeEmail').checked = true;
        }

        // Salvar novo colaborador
        function saveEmployee() {
            const name = document.getElementById('newEmployeeName').value;
            const email = document.getElementById('newEmployeeEmail').value;
            const phone = document.getElementById('newEmployeePhone').value;
            const department = document.getElementById('newEmployeeDepartment').value;
            const employeeId = document.getElementById('newEmployeeId').value.toUpperCase();
            const password = document.getElementById('newEmployeePassword').value;
            const position = document.getElementById('newEmployeePosition').value;
            const startDate = document.getElementById('newEmployeeStartDate').value;
            const role = document.getElementById('newEmployeeRole').value;
            const sendEmail = document.getElementById('sendWelcomeEmail').checked;

            // Validações
            if (!name.trim()) {
                alert('❌ Nome completo é obrigatório!');
                return;
            }

            if (!email.trim()) {
                alert('❌ Email é obrigatório!');
                return;
            }

            if (!department) {
                alert('❌ Selecione um departamento!');
                return;
            }

            if (!employeeId.trim()) {
                alert('❌ ID do colaborador é obrigatório!');
                return;
            }

            if (employees[employeeId]) {
                alert('❌ Este ID já está em uso! Escolha outro ID.');
                return;
            }

            if (!password.trim()) {
                alert('❌ Senha inicial é obrigatória!');
                return;
            }

            if (password.length < 6) {
                alert('❌ Senha deve ter pelo menos 6 caracteres!');
                return;
            }

            // Simula salvamento
            const button = event.target;
            const originalText = button.innerHTML;
            button.innerHTML = '⏳ Criando...';
            button.disabled = true;

            setTimeout(() => {
                // Adiciona o novo colaborador ao sistema
                const departmentIcon = getDepartmentIcon(department);
                employees[employeeId] = {
                    name: name,
                    department: department,
                    departmentIcon: departmentIcon,
                    email: email,
                    phone: phone,
                    position: position,
                    startDate: startDate,
                    role: role,
                    score: 0,
                    ranking: '#' + (Object.keys(employees).length + 1) + ' da equipe',
                    streak: 0,
                    profilePic: null
                };

                // Adiciona a senha do novo colaborador
                employeePasswords[employeeId] = password;

                // Salva no localStorage
                saveStoredData();

                button.innerHTML = '✅ Criado!';
                setTimeout(() => {
                    button.innerHTML = originalText;
                    button.disabled = false;
                    closeEmployeeModal();
                    
                    let message = `✅ Colaborador "${name}" criado com sucesso!\n\n`;
                    message += `🆔 ID: ${employeeId}\n`;
                    message += `🔒 Senha: ${password}\n`;
                    message += `🏢 Departamento: ${departmentIcon} ${department}\n`;
                    message += `👔 Cargo: ${position || 'Não informado'}\n`;
                    message += `\n💾 Dados salvos permanentemente!`;
                    
                    if (sendEmail) {
                        message += `\n📧 Email de boas-vindas será enviado para ${email}`;
                    }
                    
                    alert(message);
                    
                    // Atualiza a lista de usuários online se necessário
                    updateOnlineUsers();
                }, 1000);
            }, 1500);
        }

        // Função auxiliar para obter ícone do departamento
        function getDepartmentIcon(department) {
            const icons = {
                'Financeiro': '💰',
                'Marketing': '📈',
                'Tecnologia': '💻',
                'Recursos Humanos': '👥',
                'Administrativo': '📋',
                'Vendas': '🏪'
            };
            return icons[department] || '🏢';
        }

        // ===== FUNÇÕES DE USUÁRIOS ONLINE EM TEMPO REAL =====
        
        let onlineUsersData = [
            { name: 'Ana Silva', department: 'Financeiro', icon: '💰', lastSeen: new Date() },
            { name: 'Carlos Santos', department: 'Marketing', icon: '📈', lastSeen: new Date() },
            { name: 'Maria Oliveira', department: 'Tecnologia', icon: '💻', lastSeen: new Date() },
            { name: 'João Costa', department: 'RH', icon: '👥', lastSeen: new Date() }
        ];

        // Atualizar lista de usuários online
        function updateOnlineUsers() {
            const container = document.getElementById('onlineUsers');
            const countElement = document.getElementById('onlineCount');
            
            // Simula mudanças nos usuários online
            if (Math.random() > 0.7) {
                // Às vezes remove um usuário (simula logout)
                if (onlineUsersData.length > 1) {
                    onlineUsersData.pop();
                }
            } else if (Math.random() > 0.8 && onlineUsersData.length < 6) {
                // Às vezes adiciona um usuário (simula login)
                const newUsers = [
                    { name: 'Lucia Ferreira', department: 'Administrativo', icon: '📋', lastSeen: new Date() },
                    { name: 'Pedro Almeida', department: 'Vendas', icon: '🏪', lastSeen: new Date() }
                ];
                const randomUser = newUsers[Math.floor(Math.random() * newUsers.length)];
                if (!onlineUsersData.find(u => u.name === randomUser.name)) {
                    onlineUsersData.push(randomUser);
                }
            }

            // Atualiza o contador
            countElement.textContent = onlineUsersData.length;

            // Atualiza a lista
            container.innerHTML = '';
            onlineUsersData.forEach(user => {
                const userDiv = document.createElement('div');
                userDiv.className = 'flex items-center justify-between p-2 bg-white rounded-lg';
                userDiv.innerHTML = `
                    <div class="flex items-center space-x-2">
                        <div class="w-2 h-2 bg-green-500 rounded-full animate-pulse"></div>
                        <span class="text-sm font-medium">${user.name}</span>
                    </div>
                    <span class="text-xs text-gray-500">${user.icon} ${user.department}</span>
                `;
                container.appendChild(userDiv);
            });

            // Adiciona o usuário atual se não estiver na lista
            if (currentUser && !onlineUsersData.find(u => u.name === currentUser.name)) {
                const currentUserDiv = document.createElement('div');
                currentUserDiv.className = 'flex items-center justify-between p-2 bg-blue-50 rounded-lg border border-blue-200';
                currentUserDiv.innerHTML = `
                    <div class="flex items-center space-x-2">
                        <div class="w-2 h-2 bg-blue-500 rounded-full animate-pulse"></div>
                        <span class="text-sm font-medium">${currentUser.name} (Você)</span>
                    </div>
                    <span class="text-xs text-blue-600">${currentUser.departmentIcon} ${currentUser.department}</span>
                `;
                container.appendChild(currentUserDiv);
            }
        }

        // Atualizar timestamp da última atualização
        function updateLastUpdateTime() {
            const lastUpdateElement = document.getElementById('lastUpdate');
            const now = new Date();
            const seconds = Math.floor(Math.random() * 10) + 1; // 1-10 segundos
            lastUpdateElement.textContent = `${seconds} segundo${seconds > 1 ? 's' : ''}`;
        }

        // Iniciar atualizações em tempo real
        function startRealTimeUpdates() {
            // Atualiza usuários online a cada 5-8 segundos
            setInterval(() => {
                updateOnlineUsers();
                updateLastUpdateTime();
            }, Math.random() * 3000 + 5000); // 5-8 segundos

            // Atualiza timestamp a cada 2-4 segundos
            setInterval(() => {
                updateLastUpdateTime();
            }, Math.random() * 2000 + 2000); // 2-4 segundos
        }

        // ===== FUNÇÃO PARA ALTERNAR PAINEL LATERAL =====
        
        let sidebarVisible = true;

        function toggleSidebar() {
            const sidebar = document.getElementById('sidebar');
            const mainContent = document.getElementById('mainContent');
            const toggleIcon = document.getElementById('toggleIcon');
            const toggleButton = document.getElementById('toggleSidebar');
            const isMobile = window.innerWidth <= 768;
            
            sidebarVisible = !sidebarVisible;
            
            if (sidebarVisible) {
                // Mostrar painel
                sidebar.classList.remove('-translate-x-full', 'mobile-hidden');
                sidebar.classList.add('translate-x-0');
                toggleIcon.textContent = '📊';
                toggleButton.title = 'Fechar Painel de Controle';
                
                // Em desktop, ajusta margem do conteúdo
                if (!isMobile) {
                    mainContent.style.marginLeft = '320px';
                }
                
            } else {
                // Esconder painel
                sidebar.classList.remove('translate-x-0');
                sidebar.classList.add('-translate-x-full');
                if (isMobile) {
                    sidebar.classList.add('mobile-hidden');
                }
                toggleIcon.textContent = '📋';
                toggleButton.title = 'Abrir Painel de Controle';
                
                // Remove margem do conteúdo
                mainContent.style.marginLeft = '0';
            }
            
            // Animação suave do botão
            toggleButton.style.transform = 'scale(1.1)';
            setTimeout(() => {
                toggleButton.style.transform = 'scale(1)';
            }, 200);
            
            // Feedback visual adicional
            toggleButton.style.backgroundColor = sidebarVisible ? '#4f46e5' : '#059669';
            setTimeout(() => {
                toggleButton.style.backgroundColor = '#4f46e5';
            }, 300);
            
            // Salva preferência do usuário
            localStorage.setItem('gamificagestao_sidebar_visible', sidebarVisible);
        }

        // Atalho de teclado para alternar painel (Ctrl + B)
        document.addEventListener('keydown', function(e) {
            if (e.ctrlKey && e.key === 'b') {
                e.preventDefault();
                toggleSidebar();
            }
        });

        // Fechar modais clicando fora
        document.getElementById('profileModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeProfileModal();
            }
        });

        document.getElementById('reportModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeModal();
            }
        });

        document.getElementById('taskModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeTaskModal();
            }
        });

        document.getElementById('departmentModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeDepartmentModal();
            }
        });

        document.getElementById('assignModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeAssignModal();
            }
        });

        document.getElementById('employeeModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeEmployeeModal();
            }
        });

        document.getElementById('forgotPasswordModal').addEventListener('click', function(e) {
            if (e.target === this) {
                closeForgotPasswordModal();
            }
        });
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'97d14fcd52b3f632',t:'MTc1NzUzMjMzMS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
