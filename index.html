<?php
// Configuration de la base de données
class Database {
    private $host = "localhost";
    private $db_name = "shop4panel";
    private $username = "root";
    private $password = "";
    public $conn;

    public function getConnection() {
        $this->conn = null;
        try {
            $this->conn = new PDO("mysql:host=" . $this->host . ";dbname=" . $this->db_name, $this->username, $this->password);
            $this->conn->exec("set names utf8");
            $this->conn->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
        } catch(PDOException $exception) {
            echo "Connection error: " . $exception->getMessage();
        }
        return $this->conn;
    }
}

// Initialisation de la base de données
function initializeDatabase() {
    $database = new Database();
    $conn = $database->getConnection();
    
    // Création des tables si elles n'existent pas
    $sql = "
    CREATE TABLE IF NOT EXISTS users (
        id INT PRIMARY KEY AUTO_INCREMENT,
        username VARCHAR(50) UNIQUE NOT NULL,
        email VARCHAR(100) UNIQUE NOT NULL,
        password VARCHAR(255) NOT NULL,
        full_name VARCHAR(100),
        balance DECIMAL(10,2) DEFAULT 0.00,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
        last_login TIMESTAMP NULL,
        status ENUM('active', 'inactive') DEFAULT 'active'
    );
    
    CREATE TABLE IF NOT EXISTS products (
        id INT PRIMARY KEY AUTO_INCREMENT,
        name VARCHAR(100) NOT NULL,
        type ENUM('code', 'm3u', 'special') NOT NULL,
        duration VARCHAR(20) NOT NULL,
        price DECIMAL(10,2) NOT NULL,
        stock INT DEFAULT 0,
        description TEXT,
        featured BOOLEAN DEFAULT FALSE,
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    
    CREATE TABLE IF NOT EXISTS transactions (
        id INT PRIMARY KEY AUTO_INCREMENT,
        user_id INT,
        product_id INT,
        quantity INT DEFAULT 1,
        total_amount DECIMAL(10,2),
        transaction_type ENUM('purchase', 'recharge', 'refund'),
        status ENUM('pending', 'completed', 'failed'),
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    
    CREATE TABLE IF NOT EXISTS tickets (
        id INT PRIMARY KEY AUTO_INCREMENT,
        user_id INT,
        subject VARCHAR(255),
        message TEXT,
        priority ENUM('low', 'medium', 'high', 'urgent'),
        status ENUM('open', 'in_progress', 'resolved', 'closed'),
        created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ";
    
    try {
        $conn->exec($sql);
        
        // Vérifier si les produits existent déjà
        $checkProducts = $conn->query("SELECT COUNT(*) FROM products")->fetchColumn();
        
        if ($checkProducts == 0) {
            // Insertion des produits
            $insertProducts = "
            INSERT INTO products (name, type, duration, price, stock, description, featured) VALUES
            ('L.P.T.V Active Code', 'code', '12 Mois', 68.00, 68, 'CODE IPTV 12 MOIS', 1),
            ('L.P.T.V M3U', 'm3u', '12 Mois', 75.00, 75, 'M3U 12MOIS ON DEMANDE', 0),
            ('L.P.T.V Active Code', 'code', '6 Mois', 39.00, 39, 'CODE IPTV 6 MOIS', 0),
            ('L.P.T.V M3U', 'm3u', '6 Mois', 66.00, 66, 'M3U 6 MOIS ON DEMANDE', 0),
            ('L.P.T.V Active Code', 'code', '3 Mois', 36.00, 36, 'CODE IPTV 3 MOIS', 0),
            ('L.P.T.V M3U', 'm3u', '3 Mois', 64.00, 64, 'M3U 3 MOIS ON DEMANDE', 0),
            ('L.P.T.V Active Code', 'code', '1 Mois', 34.00, 34, 'CODE IPTV 1 MOIS', 0),
            ('L.P.T.V M3U', 'm3u', '1 Mois', 12.00, 12, 'M3U 1 MOIS ON DEMANDE', 0),
            ('عرض استثنائية', 'special', 'Special', 41.00, 41, 'عرض استثنائية', 0),
            ('Bein sport تجديد', 'special', 'Renewal', 7.00, 7, 'Bein sport تجديد اشتراكات', 0),
            ('PANEL RECHARGE IPTV', 'special', 'Recharge', 83.00, 83, 'PANEL RECHARGE IPTV', 0),
            ('SHARING MANGO', 'special', 'Sharing', 10.00, 10, 'SHARING MANGO', 0),
            ('ACTIVATION MAC TV', 'special', 'Activation', 74.00, 74, 'ACTIVATION MAC TV', 0),
            ('SHARING', 'special', 'Sharing', 13.00, 13, 'SHARING', 0),
            ('Prince TV PRO', 'special', 'PRO', 7.00, 7, 'Prince TV PRO', 0),
            ('Shahid 12 MOIS', 'special', '12 Mois', 3.00, 3, 'Shahid 12 MOIS واحد 5...', 0);
            ";
            $conn->exec($insertProducts);
        }
        
        // Vérifier si l'admin existe
        $checkAdmin = $conn->query("SELECT COUNT(*) FROM users WHERE username = 'admin'")->fetchColumn();
        
        if ($checkAdmin == 0) {
            // Utilisateur de test
            $hashedPassword = password_hash('admin123', PASSWORD_DEFAULT);
            $insertAdmin = "INSERT INTO users (username, email, password, full_name, balance) VALUES 
            ('admin', 'admin@shop4panel.com', '$hashedPassword', 'Admin Shop4Panel', 2580.00)";
            $conn->exec($insertAdmin);
        }
        
    } catch(PDOException $e) {
        // Les tables existent probablement déjà
    }
}

// Traitement des actions d'authentification
if ($_SERVER['REQUEST_METHOD'] === 'POST' && isset($_GET['action'])) {
    $database = new Database();
    $conn = $database->getConnection();
    
    if ($_GET['action'] === 'login') {
        $data = json_decode(file_get_contents('php://input'), true);
        $email = $data['email'];
        $password = $data['password'];
        
        $query = "SELECT * FROM users WHERE (email = :email OR username = :email) AND status = 'active'";
        $stmt = $conn->prepare($query);
        $stmt->bindParam(':email', $email);
        $stmt->execute();
        
        if ($stmt->rowCount() == 1) {
            $user = $stmt->fetch(PDO::FETCH_ASSOC);
            if (password_verify($password, $user['password'])) {
                // Mettre à jour la dernière connexion
                $updateQuery = "UPDATE users SET last_login = NOW() WHERE id = :id";
                $updateStmt = $conn->prepare($updateQuery);
                $updateStmt->bindParam(':id', $user['id']);
                $updateStmt->execute();
                
                // Démarrer la session
                session_start();
                $_SESSION['user_id'] = $user['id'];
                $_SESSION['username'] = $user['username'];
                $_SESSION['full_name'] = $user['full_name'];
                $_SESSION['balance'] = $user['balance'];
                
                echo json_encode(['success' => true, 'message' => 'Connexion réussie', 'user' => $user]);
            } else {
                echo json_encode(['success' => false, 'message' => 'Mot de passe incorrect']);
            }
        } else {
            echo json_encode(['success' => false, 'message' => 'Utilisateur non trouvé']);
        }
    }
    
    if ($_GET['action'] === 'register') {
        $data = json_decode(file_get_contents('php://input'), true);
        $fullName = $data['fullName'];
        $username = $data['username'];
        $email = $data['email'];
        $password = $data['password'];
        
        // Vérifier si l'utilisateur existe déjà
        $checkQuery = "SELECT id FROM users WHERE email = :email OR username = :username";
        $checkStmt = $conn->prepare($checkQuery);
        $checkStmt->bindParam(':email', $email);
        $checkStmt->bindParam(':username', $username);
        $checkStmt->execute();
        
        if ($checkStmt->rowCount() > 0) {
            echo json_encode(['success' => false, 'message' => 'Email ou nom d\'utilisateur déjà utilisé']);
        } else {
            $hashedPassword = password_hash($password, PASSWORD_DEFAULT);
            $insertQuery = "INSERT INTO users (username, email, password, full_name) VALUES (:username, :email, :password, :full_name)";
            $insertStmt = $conn->prepare($insertQuery);
            $insertStmt->bindParam(':username', $username);
            $insertStmt->bindParam(':email', $email);
            $insertStmt->bindParam(':password', $hashedPassword);
            $insertStmt->bindParam(':full_name', $fullName);
            
            if ($insertStmt->execute()) {
                echo json_encode(['success' => true, 'message' => 'Compte créé avec succès']);
            } else {
                echo json_encode(['success' => false, 'message' => 'Erreur lors de la création du compte']);
            }
        }
    }
    
    exit;
}

// Initialiser la base de données
initializeDatabase();

// Vérifier si l'utilisateur est connecté
session_start();
$isLoggedIn = isset($_SESSION['user_id']);

// Déterminer la langue
$lang = isset($_GET['lang']) ? $_GET['lang'] : 'fr';
$languages = [
    'fr' => 'Français',
    'ar' => 'العربية',
    'en' => 'English'
];

// Contenu multilingue
$content = [
    'fr' => [
        'title' => 'Shop4Panel - Panel IPTV Professionnel',
        'description' => 'SHOP4PANEL propose des tarifs les moins chers sur le marché. Nous aidons au développement des petits et grands revendeurs partout au Maroc.',
        'login' => 'Connexion',
        'register' => 'Inscription',
        'dashboard' => 'Tableau de bord',
        'logout' => 'Déconnexion',
        'welcome' => 'Bienvenue sur Shop4Panel',
        'features' => 'Nos Services',
        'feature1' => 'Tarifs Compétitifs',
        'feature1_desc' => 'Les meilleurs prix du marché pour tous vos besoins IPTV',
        'feature2' => 'Support 24/7',
        'feature2_desc' => 'Notre équipe est disponible à tout moment pour vous assister',
        'feature3' => 'Revendeurs',
        'feature3_desc' => 'Programme spécial pour les revendeurs avec des marges avantageuses',
        'about' => 'À Propos',
        'about_text' => 'Shop4Panel est une plateforme leader dans la distribution de services IPTV au Maroc. Nous nous engageons à fournir des solutions de qualité à des prix imbattables.',
        'contact' => 'Contactez-nous',
        'email' => 'Email',
        'phone' => 'Téléphone',
        'address' => 'Adresse',
        'copyright' => 'Tous droits réservés'
    ],
    'ar' => [
        'title' => 'Shop4Panel - لوحة IPTV الاحترافية',
        'description' => 'SHOP4PANEL تقدم أرخص الأسعار في السوق. نحن نساعد في تطوير البائعين الصغار والكبار في جميع أنحاء المغرب.',
        'login' => 'تسجيل الدخول',
        'register' => 'إنشاء حساب',
        'dashboard' => 'لوحة التحكم',
        'logout' => 'تسجيل الخروج',
        'welcome' => 'مرحبا بكم في Shop4Panel',
        'features' => 'خدماتنا',
        'feature1' => 'أسعار تنافسية',
        'feature1_desc' => 'أفضل الأسعار في السوق لجميع احتياجاتك في IPTV',
        'feature2' => 'دعم 24/7',
        'feature2_desc' => 'فريقنا متاح في أي وقت لمساعدتك',
        'feature3' => 'البائعون',
        'feature3_desc' => 'برنامج خاص للبائعين مع هوامش ربح مغرية',
        'about' => 'من نحن',
        'about_text' => 'Shop4Panel هي منصة رائدة في توزيع خدمات IPTV في المغرب. نحن ملتزمون بتقديم حلول عالية الجودة بأسعار لا تقبل المنافسة.',
        'contact' => 'اتصل بنا',
        'email' => 'البريد الإلكتروني',
        'phone' => 'الهاتف',
        'address' => 'العنوان',
        'copyright' => 'جميع الحقوق محفوظة'
    ],
    'en' => [
        'title' => 'Shop4Panel - Professional IPTV Panel',
        'description' => 'SHOP4PANEL offers the cheapest prices on the market. We help develop small and large resellers throughout Morocco.',
        'login' => 'Login',
        'register' => 'Register',
        'dashboard' => 'Dashboard',
        'logout' => 'Logout',
        'welcome' => 'Welcome to Shop4Panel',
        'features' => 'Our Services',
        'feature1' => 'Competitive Prices',
        'feature1_desc' => 'The best market prices for all your IPTV needs',
        'feature2' => '24/7 Support',
        'feature2_desc' => 'Our team is available at any time to assist you',
        'feature3' => 'Resellers',
        'feature3_desc' => 'Special program for resellers with attractive margins',
        'about' => 'About Us',
        'about_text' => 'Shop4Panel is a leading platform in the distribution of IPTV services in Morocco. We are committed to providing quality solutions at unbeatable prices.',
        'contact' => 'Contact Us',
        'email' => 'Email',
        'phone' => 'Phone',
        'address' => 'Address',
        'copyright' => 'All rights reserved'
    ]
];

$currentContent = $content[$lang];
?>
<!DOCTYPE html>
<html lang="<?php echo $lang; ?>" dir="<?php echo $lang == 'ar' ? 'rtl' : 'ltr'; ?>">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title><?php echo $currentContent['title']; ?></title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary-color: #5726d4;
            --secondary-color: #8a63d2;
            --accent-color: #ff6b35;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }
        
        .navbar {
            background: rgba(255, 255, 255, 0.95);
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .hero-section {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            margin-top: 30px;
            padding: 50px;
            text-align: center;
        }
        
        .feature-card {
            background: white;
            border-radius: 15px;
            padding: 30px;
            margin: 15px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border: 2px solid transparent;
            transition: all 0.3s ease;
            text-align: center;
            height: 100%;
        }
        
        .feature-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0,0,0,0.15);
            border-color: var(--primary-color);
        }
        
        .feature-icon {
            font-size: 3rem;
            color: var(--primary-color);
            margin-bottom: 20px;
        }
        
        .language-switcher {
            margin-right: 15px;
        }
        
        .btn-primary-custom {
            background: linear-gradient(45deg, var(--primary-color), var(--secondary-color));
            color: white;
            border: none;
            padding: 10px 25px;
            border-radius: 25px;
            font-weight: 600;
            transition: all 0.3s ease;
        }
        
        .btn-primary-custom:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(87,38,212,0.4);
            color: white;
        }
        
        .section-title {
            color: var(--primary-color);
            font-weight: 800;
            margin: 50px 0 30px;
            padding-bottom: 10px;
            border-bottom: 3px solid var(--primary-color);
            text-align: center;
        }
        
        /* Styles pour le tableau de bord */
        .dashboard-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
            min-height: 90vh;
            margin-top: 20px;
        }
        
        .header-bar {
            background: var(--primary-color);
            color: white;
            padding: 15px 25px;
            border-bottom: 3px solid var(--accent-color);
        }
        
        .stats-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border: 2px solid transparent;
            transition: all 0.3s ease;
        }
        
        .product-card {
            background: white;
            border-radius: 15px;
            padding: 20px;
            margin: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.08);
            border: 2px solid #f0f0f0;
            transition: all 0.3s ease;
            text-align: center;
            position: relative;
            overflow: hidden;
        }
        
        /* Styles pour la page de connexion */
        .login-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
            width: 100%;
            max-width: 400px;
            margin: 50px auto;
        }
        
        .login-header {
            background: var(--primary-color);
            color: white;
            padding: 30px;
            text-align: center;
        }
    </style>
</head>
<body>
    <!-- Navigation -->
    <nav class="navbar navbar-expand-lg">
        <div class="container">
            <a class="navbar-brand fw-bold fs-3" href="?lang=<?php echo $lang; ?>">
                <i class="fas fa-tv me-2"></i>SHOP4PANEL
            </a>
            
            <div class="d-flex align-items-center">
                <!-- Sélecteur de langue -->
                <div class="language-switcher dropdown">
                    <button class="btn btn-outline-primary dropdown-toggle" type="button" data-bs-toggle="dropdown">
                        <i class="fas fa-globe me-1"></i> <?php echo $languages[$lang]; ?>
                    </button>
                    <ul class="dropdown-menu">
                        <li><a class="dropdown-item" href="?lang=fr">Français</a></li>
                        <li><a class="dropdown-item" href="?lang=ar">العربية</a></li>
                        <li><a class="dropdown-item" href="?lang=en">English</a></li>
                    </ul>
                </div>
                
                <!-- Menu utilisateur -->
                <?php if ($isLoggedIn): ?>
                    <div class="dropdown">
                        <button class="btn btn-primary-custom dropdown-toggle" type="button" data-bs-toggle="dropdown">
                            <i class="fas fa-user me-2"></i><?php echo $_SESSION['username']; ?>
                        </button>
                        <ul class="dropdown-menu">
                            <li><a class="dropdown-item" href="?page=dashboard&lang=<?php echo $lang; ?>"><?php echo $currentContent['dashboard']; ?></a></li>
                            <li><hr class="dropdown-divider"></li>
                            <li><a class="dropdown-item" href="?action=logout&lang=<?php echo $lang; ?>"><?php echo $currentContent['logout']; ?></a></li>
                        </ul>
                    </div>
                <?php else: ?>
                    <a href="?page=login&lang=<?php echo $lang; ?>" class="btn btn-outline-primary me-2"><?php echo $currentContent['login']; ?></a>
                    <a href="?page=register&lang=<?php echo $lang; ?>" class="btn btn-primary-custom"><?php echo $currentContent['register']; ?></a>
                <?php endif; ?>
            </div>
        </div>
    </nav>

    <!-- Contenu principal -->
    <div class="container">
        <?php
        // Gestion des pages
        $page = isset($_GET['page']) ? $_GET['page'] : 'home';
        
        if ($isLoggedIn && $page === 'home') {
            $page = 'dashboard';
        }
        
        switch($page) {
            case 'dashboard':
                include 'dashboard_content.php';
                break;
            case 'login':
                include 'login_content.php';
                break;
            case 'register':
                include 'register_content.php';
                break;
            default:
                include 'home_content.php';
                break;
        }
        ?>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/js/bootstrap.bundle.min.js"></script>
    <script>
        // Gestion des formulaires d'authentification
        document.addEventListener('DOMContentLoaded', function() {
            const loginForm = document.getElementById('loginFormData');
            const registerForm = document.getElementById('signupFormData');
            
            if (loginForm) {
                loginForm.addEventListener('submit', async function(e) {
                    e.preventDefault();
                    
                    const email = document.getElementById('loginEmail').value;
                    const password = document.getElementById('loginPassword').value;
                    
                    try {
                        const response = await fetch('?action=login&lang=<?php echo $lang; ?>', {
                            method: 'POST',
                            headers: {
                                'Content-Type': 'application/json'
                            },
                            body: JSON.stringify({ email, password })
                        });
                        
                        const data = await response.json();
                        
                        if (data.success) {
                            window.location.href = '?page=dashboard&lang=<?php echo $lang; ?>';
                        } else {
                            showError(data.message);
                        }
                    } catch (error) {
                        showError('Erreur de connexion. Veuillez réessayer.');
                    }
                });
            }
            
            if (registerForm) {
                registerForm.addEventListener('submit', async function(e) {
                    e.preventDefault();
                    
                    const fullName = document.getElementById('fullName').value;
                    const username = document.getElementById('username').value;
                    const email = document.getElementById('email').value;
                    const password = document.getElementById('password').value;
                    const confirmPassword = document.getElementById('confirmPassword').value;
                    
                    if (password !== confirmPassword) {
                        showError('Les mots de passe ne correspondent pas.');
                        return;
                    }
                    
                    try {
                        const response = await fetch('?action=register&lang=<?php echo $lang; ?>', {
                            method: 'POST',
                            headers: {
                                'Content-Type': 'application/json'
                            },
                            body: JSON.stringify({ fullName, username, email, password })
                        });
                        
                        const data = await response.json();
                        
                        if (data.success) {
                            showError('Compte créé avec succès! Vous pouvez maintenant vous connecter.', 'success');
                            setTimeout(() => {
                                window.location.href = '?page=login&lang=<?php echo $lang; ?>';
                            }, 2000);
                        } else {
                            showError(data.message);
                        }
                    } catch (error) {
                        showError('Erreur lors de l\'inscription. Veuillez réessayer.');
                    }
                });
            }
            
            function showError(message, type = 'error') {
                // Créer une alerte si elle n'existe pas
                let errorAlert = document.getElementById('errorAlert');
                if (!errorAlert) {
                    errorAlert = document.createElement('div');
                    errorAlert.id = 'errorAlert';
                    errorAlert.className = 'alert alert-danger mt-3';
                    document.querySelector('.login-body').appendChild(errorAlert);
                }
                
                errorAlert.textContent = message;
                errorAlert.className = `alert alert-${type === 'success' ? 'success' : 'danger'} mt-3`;
                errorAlert.style.display = 'block';
                
                setTimeout(() => {
                    errorAlert.style.display = 'none';
                }, 5000);
            }
        });
    </script>
</body>
</html>

<?php
// Déconnexion
if (isset($_GET['action']) && $_GET['action'] === 'logout') {
    session_destroy();
    header('Location: ?lang=' . $lang);
    exit;
}

// Contenu de la page d'accueil
ob_start();
?>
<div class="hero-section">
    <h1 class="display-4 fw-bold text-primary mb-4"><?php echo $currentContent['welcome']; ?></h1>
    <p class="lead mb-4"><?php echo $currentContent['description']; ?></p>
    <?php if (!$isLoggedIn): ?>
        <a href="?page=register&lang=<?php echo $lang; ?>" class="btn btn-primary-custom btn-lg"><?php echo $currentContent['register']; ?></a>
    <?php else: ?>
        <a href="?page=dashboard&lang=<?php echo $lang; ?>" class="btn btn-primary-custom btn-lg"><?php echo $currentContent['dashboard']; ?></a>
    <?php endif; ?>
</div>

<h2 class="section-title"><?php echo $currentContent['features']; ?></h2>

<div class="row">
    <div class="col-md-4">
        <div class="feature-card">
            <div class="feature-icon">
                <i class="fas fa-tags"></i>
            </div>
            <h4><?php echo $currentContent['feature1']; ?></h4>
            <p><?php echo $currentContent['feature1_desc']; ?></p>
        </div>
    </div>
    <div class="col-md-4">
        <div class="feature-card">
            <div class="feature-icon">
                <i class="fas fa-headset"></i>
            </div>
            <h4><?php echo $currentContent['feature2']; ?></h4>
            <p><?php echo $currentContent['feature2_desc']; ?></p>
        </div>
    </div>
    <div class="col-md-4">
        <div class="feature-card">
            <div class="feature-icon">
                <i class="fas fa-users"></i>
            </div>
            <h4><?php echo $currentContent['feature3']; ?></h4>
            <p><?php echo $currentContent['feature3_desc']; ?></p>
        </div>
    </div>
</div>

<div class="row mt-5">
    <div class="col-md-6">
        <h3 class="mb-4"><?php echo $currentContent['about']; ?></h3>
        <p><?php echo $currentContent['about_text']; ?></p>
    </div>
    <div class="col-md-6">
        <h3 class="mb-4"><?php echo $currentContent['contact']; ?></h3>
        <p><strong><?php echo $currentContent['email']; ?>:</strong> contact@shop4panel.com</p>
        <p><strong><?php echo $currentContent['phone']; ?>:</strong> +212 6 12 34 56 78</p>
        <p><strong><?php echo $currentContent['address']; ?>:</strong> Casablanca, Maroc</p>
    </div>
</div>

<footer class="text-center mt-5 py-4 text-muted">
    <p>&copy; 2024 Shop4Panel - <?php echo $currentContent['copyright']; ?></p>
</footer>
<?php
$home_content = ob_get_clean();

// Contenu de la page de connexion
ob_start();
?>
<div class="login-container">
    <div class="login-header">
        <div class="logo">
            <i class="fas fa-tv me-2"></i>SHOP4PANEL
        </div>
        <p class="mb-0"><?php echo $currentContent['title']; ?></p>
    </div>
    
    <div class="login-body">
        <h4 class="text-center mb-4"><?php echo $currentContent['login']; ?></h4>
        
        <div class="alert alert-warning text-center">
            <i class="fas fa-exclamation-triangle me-2"></i>
            اقل رصيد 1000 درهم
        </div>
        
        <form id="loginFormData">
            <div class="mb-3">
                <label for="loginEmail" class="form-label">Email ou Nom d'utilisateur</label>
                <input type="text" class="form-control" id="loginEmail" required>
            </div>
            
            <div class="mb-3">
                <label for="loginPassword" class="form-label">Mot de passe</label>
                <input type="password" class="form-control" id="loginPassword" required>
            </div>
            
            <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input" id="rememberMe">
                <label class="form-check-label" for="rememberMe">Se souvenir de moi</label>
            </div>
            
            <button type="submit" class="btn btn-primary-custom w-100 mb-3">
                <i class="fas fa-sign-in-alt me-2"></i><?php echo $currentContent['login']; ?>
            </button>
        </form>
        
        <div class="text-center">
            <a href="#" class="text-muted">Mot de passe oublié?</a>
        </div>
        
        <hr>
        
        <div class="text-center">
            <p class="text-muted">Nouveau sur Shop4Panel?</p>
            <a href="?page=register&lang=<?php echo $lang; ?>" class="btn btn-outline-primary w-100">
                <i class="fas fa-user-plus me-2"></i><?php echo $currentContent['register']; ?>
            </a>
        </div>
    </div>
</div>
<?php
$login_content = ob_get_clean();

// Contenu de la page d'inscription
ob_start();
?>
<div class="login-container">
    <div class="login-header">
        <div class="logo">
            <i class="fas fa-tv me-2"></i>SHOP4PANEL
        </div>
        <p class="mb-0"><?php echo $currentContent['title']; ?></p>
    </div>
    
    <div class="login-body">
        <h4 class="text-center mb-4"><?php echo $currentContent['register']; ?></h4>
        
        <form id="signupFormData">
            <div class="mb-3">
                <label for="fullName" class="form-label">Nom complet</label>
                <input type="text" class="form-control" id="fullName" required>
            </div>
            
            <div class="mb-3">
                <label for="username" class="form-label">Nom d'utilisateur</label>
                <input type="text" class="form-control" id="username" required>
            </div>
            
            <div class="mb-3">
                <label for="email" class="form-label">Email</label>
                <input type="email" class="form-control" id="email" required>
            </div>
            
            <div class="mb-3">
                <label for="password" class="form-label">Mot de passe</label>
                <input type="password" class="form-control" id="password" required>
            </div>
            
            <div class="mb-3">
                <label for="confirmPassword" class="form-label">Confirmer le mot de passe</label>
                <input type="password" class="form-control" id="confirmPassword" required>
            </div>
            
            <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input" id="agreeTerms" required>
                <label class="form-check-label" for="agreeTerms">
                    J'accepte les <a href="#">conditions d'utilisation</a>
                </label>
            </div>
            
            <button type="submit" class="btn btn-primary-custom w-100 mb-3">
                <i class="fas fa-user-plus me-2"></i><?php echo $currentContent['register']; ?>
            </button>
        </form>
        
        <div class="text-center">
            <a href="?page=login&lang=<?php echo $lang; ?>" class="btn btn-link text-muted">
                <i class="fas fa-arrow-left me-2"></i>Retour à la connexion
            </a>
        </div>
    </div>
</div>
<?php
$register_content = ob_get_clean();

// Contenu du tableau de bord
ob_start();
?>
<div class="dashboard-container">
    <!-- Header -->
    <div class="header-bar">
        <div class="row align-items-center">
            <div class="col-md-6">
                <div class="logo">
                    <i class="fas fa-tv me-2"></i>SHOP4PANEL
                </div>
            </div>
            <div class="col-md-6 text-md-end">
                <div class="user-info">
                    <i class="fas fa-user me-2"></i><?php echo $_SESSION['full_name']; ?>
                </div>
            </div>
        </div>
    </div>

    <!-- Alert Messages -->
    <div class="alert alert-warning text-center m-3">
        <i class="fas fa-exclamation-triangle me-2"></i>
        اجباري اجباري لا تحمل مسؤولية أي
    </div>
    
    <div class="alert alert-success text-center m-3">
        <i class="fas fa-wallet me-2"></i>
        درهم 1000 اقل رصيد
    </div>

    <!-- Stats Section -->
    <div class="row">
        <div class="col-md-3">
            <div class="stats-card text-center">
                <p class="stats-label">Clients Actifs</p>
                <p class="stats-number">68</p>
            </div>
        </div>
        <div class="col-md-3">
            <div class="stats-card text-center">
                <p class="stats-label">Produits Vendus</p>
                <p class="stats-number">156</p>
            </div>
        </div>
        <div class="col-md-3">
            <div class="stats-card text-center">
                <p class="stats-label">Revenu Total</p>
                <p class="stats-number">2,580€</p>
            </div>
        </div>
        <div class="col-md-3">
            <div class="stats-card text-center">
                <p class="stats-label">Tickets Ouverts</p>
                <p class="stats-number">3</p>
            </div>
        </div>
    </div>

    <!-- Products Grid -->
    <h3 class="section-title">LINK 4 PANEL - PRODUITS IPTV</h3>
    
    <div class="row">
        <?php
        $database = new Database();
        $conn = $database->getConnection();
        $query = "SELECT * FROM products ORDER BY featured DESC, id ASC";
        $stmt = $conn->prepare($query);
        $stmt->execute();
        
        while ($product = $stmt->fetch(PDO::FETCH_ASSOC)) {
            echo '
            <div class="col-xl-3 col-lg-4 col-md-6">
                <div class="product-card' . ($product['featured'] ? ' featured' : '') . '">
                    ' . ($product['featured'] ? '<div class="product-badge">POPULAIRE</div>' : '') . '
                    <div class="product-title">' . $product['name'] . '</div>
                    <div class="product-price">' . $product['duration'] . '</div>
                    <div class="product-stock">' . $product['stock'] . ' Produits</div>
                    <div class="product-description">
                        ' . $product['description'] . '
                    </div>
                    <button class="btn btn-primary-custom w-100">
                        <i class="fas fa-shopping-cart me-2"></i>ACHETER
                    </button>
                </div>
            </div>';
        }
        ?>
    </div>

    <!-- Footer -->
    <div class="text-center mt-4 p-3 text-muted">
        <small>© 2024 Shop4Panel - Tous droits réservés | Panel IPTV Professionnel</small>
    </div>
</div>
<?php
$dashboard_content = ob_get_clean();

// Inclure le contenu approprié
switch($page) {
    case 'dashboard':
        echo $dashboard_content;
        break;
    case 'login':
        echo $login_content;
        break;
    case 'register':
        echo $register_content;
        break;
    default:
        echo $home_content;
        break;
}
?>
