<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=5.0">
    <meta name="theme-color" content="#1B5E20">
    <meta name="description" content="JAMBO - The world's most accessible messaging platform. Connecting everyone, everywhere.">
    <title>JAMBO | Connect Beyond Limits</title>
    
    <!-- PWA Manifest -->
    <link rel="manifest" href="/manifest.json">
    <link rel="apple-touch-icon" href="/icons/icon-192x192.png">
    <link rel="icon" type="image/png" href="/icons/icon-72x72.png">
    
    <!-- Fonts -->
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;600;800&family=Open+Dyslexic&family=Ubuntu+Mono&family=Noto+Sans+SC&family=Noto+Sans+Arabic&display=swap" rel="stylesheet">
    
    <!-- Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    
    <style>
        :root {
            /* Core Colors */
            --primary: #1B5E20;
            --primary-light: #2E7D32;
            --secondary: #FFB300;
            --secondary-light: #FFC107;
            --accent: #00695C;
            --accent-light: #00897B;
            
            /* Semantic Colors */
            --success: #4CAF50;
            --warning: #FF9800;
            --error: #F44336;
            --info: #2196F3;
            
            /* Backgrounds */
            --bg-dark: #0a0f0d;
            --bg-card: rgba(255, 255, 255, 0.05);
            --bg-glass: rgba(255, 255, 255, 0.08);
            --bg-hover: rgba(255, 255, 255, 0.12);
            
            /* Text */
            --text-primary: #ffffff;
            --text-secondary: rgba(255, 255, 255, 0.7);
            --text-muted: rgba(255, 255, 255, 0.5);
            
            /* Spacing */
            --space-xs: 4px;
            --space-sm: 8px;
            --space-md: 16px;
            --space-lg: 24px;
            --space-xl: 32px;
            
            /* Radius */
            --radius-sm: 8px;
            --radius-md: 12px;
            --radius-lg: 16px;
            --radius-xl: 24px;
            
            /* Shadows */
            --shadow-sm: 0 2px 8px rgba(0,0,0,0.1);
            --shadow-md: 0 4px 16px rgba(0,0,0,0.2);
            --shadow-lg: 0 8px 32px rgba(0,0,0,0.3);
            --shadow-glow: 0 0 20px rgba(255, 179, 0, 0.3);
            
            /* Animation */
            --transition-fast: 0.15s ease;
            --transition-base: 0.3s ease;
            --transition-slow: 0.5s ease;
            
            /* Accessibility */
            --focus-ring: 0 0 0 3px rgba(255, 179, 0, 0.5);
            --min-touch-target: 44px;
        }

        /* Reset & Base */
        *, *::before, *::after {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        html {
            font-size: 16px;
            scroll-behavior: smooth;
        }

        body {
            font-family: 'Outfit', -apple-system, BlinkMacSystemFont, sans-serif;
            background: var(--bg-dark);
            color: var(--text-primary);
            min-height: 100vh;
            line-height: 1.6;
            overflow-x: hidden;
        }

        /* Accessibility Modes */
        body.dyslexia-mode { font-family: 'Open Dyslexic', sans-serif !important; }
        body.high-contrast { 
            --bg-dark: #000000;
            --bg-card: #000000;
            --text-primary: #ffffff;
            --primary: #00ff00;
            --secondary: #ffff00;
            filter: contrast(1.5);
        }
        body.large-text { font-size: 20px; }
        body.large-text .btn { font-size: 1.1rem; padding: 20px; }
        body.reduce-motion * { animation-duration: 0.01ms !important; transition-duration: 0.01ms !important; }

        /* Animated Background */
        .bg-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            background: linear-gradient(135deg, #0a0f0d 0%, #1B5E20 50%, #0d3328 100%);
        }

        .bg-particles {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            pointer-events: none;
        }

        .particle {
            position: absolute;
            background: var(--secondary);
            border-radius: 50%;
            opacity: 0.3;
            animation: float 15s infinite ease-in-out;
        }

        @keyframes float {
            0%, 100% { transform: translateY(100vh) scale(0); opacity: 0; }
            10% { opacity: 0.3; }
            90% { opacity: 0.3; }
            100% { transform: translateY(-10vh) scale(1); opacity: 0; }
        }

        /* App Container */
        #app {
            width: 100%;
            max-width: 480px;
            min-height: 100vh;
            margin: 0 auto;
            background: rgba(10, 15, 13, 0.95);
            position: relative;
            display: flex;
            flex-direction: column;
            backdrop-filter: blur(20px);
        }

        @media (min-width: 481px) {
            #app {
                min-height: 90vh;
                margin: 5vh auto;
                border-radius: var(--radius-xl);
                box-shadow: var(--shadow-lg), 0 0 60px rgba(27, 94, 32, 0.3);
                border: 1px solid rgba(255, 255, 255, 0.1);
            }
        }

        /* Screen Management */
        .screen {
            display: none;
            flex-direction: column;
            flex: 1;
            padding: var(--space-lg);
            animation: screenEnter 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            overflow-y: auto;
            position: relative;
        }

        .screen.active {
            display: flex;
        }

        @keyframes screenEnter {
            from { opacity: 0; transform: translateX(20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        /* Typography */
        h1 { 
            font-size: 2.5rem; 
            font-weight: 800; 
            background: linear-gradient(135deg, var(--secondary), var(--secondary-light));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: var(--space-sm);
            letter-spacing: -0.02em;
        }

        h2 { 
            font-size: 1.75rem; 
            font-weight: 700; 
            margin-bottom: var(--space-md);
            color: var(--text-primary);
        }

        h3 { font-size: 1.25rem; font-weight: 600; }
        
        .subtitle { 
            color: var(--text-secondary); 
            font-size: 1rem;
            margin-bottom: var(--space-xl);
            line-height: 1.6;
        }

        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            justify-content: center;
            gap: var(--space-sm);
            padding: var(--space-md) var(--space-lg);
            border: none;
            border-radius: var(--radius-md);
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all var(--transition-base);
            min-height: var(--min-touch-target);
            position: relative;
            overflow: hidden;
        }

        .btn:focus-visible {
            outline: none;
            box-shadow: var(--focus-ring);
        }

        .btn-primary {
            background: linear-gradient(135deg, var(--secondary), var(--secondary-light));
            color: #000;
            box-shadow: var(--shadow-md), var(--shadow-glow);
        }

        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg), 0 0 30px rgba(255, 179, 0, 0.4);
        }

        .btn-primary:active { transform: translateY(0); }

        .btn-secondary {
            background: var(--bg-glass);
            color: var(--text-primary);
            border: 1px solid rgba(255,255,255,0.2);
        }

        .btn-secondary:hover {
            background: var(--bg-hover);
            border-color: rgba(255,255,255,0.3);
        }

        .btn-ghost {
            background: transparent;
            color: var(--text-secondary);
        }

        .btn-ghost:hover { color: var(--text-primary); }

        .btn-success {
            background: var(--success);
            color: white;
        }

        .btn-block { width: 100%; }

        .btn-lg {
            padding: var(--space-lg);
            font-size: 1.1rem;
        }

        /* Inputs */
        .input-group {
            margin-bottom: var(--space-lg);
            position: relative;
        }

        .input-label {
            display: block;
            margin-bottom: var(--space-sm);
            font-size: 0.875rem;
            font-weight: 500;
            color: var(--text-secondary);
        }

        .input-field {
            width: 100%;
            padding: var(--space-md);
            background: var(--bg-card);
            border: 2px solid rgba(255,255,255,0.1);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: 1rem;
            transition: all var(--transition-base);
            min-height: var(--min-touch-target);
        }

        .input-field:hover {
            border-color: rgba(255,255,255,0.2);
        }

        .input-field:focus {
            outline: none;
            border-color: var(--secondary);
            background: var(--bg-hover);
            box-shadow: var(--shadow-glow);
        }

        .input-field::placeholder {
            color: var(--text-muted);
        }

        .input-error {
            border-color: var(--error) !important;
        }

        .error-message {
            color: var(--error);
            font-size: 0.875rem;
            margin-top: var(--space-xs);
            display: flex;
            align-items: center;
            gap: var(--space-xs);
        }

        /* Phone Input */
        .phone-input-wrapper {
            display: flex;
            gap: var(--space-sm);
        }

        .country-select {
            width: 120px;
            padding: var(--space-md);
            background: var(--bg-card);
            border: 2px solid rgba(255,255,255,0.1);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: 1rem;
            cursor: pointer;
            appearance: none;
            background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24' viewBox='0 0 24 24' fill='none' stroke='white' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3E%3Cpolyline points='6 9 12 15 18 9'%3E%3C/polyline%3E%3C/svg%3E");
            background-repeat: no-repeat;
            background-position: right 8px center;
            background-size: 20px;
        }

        /* Language Selection */
        .lang-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--space-md);
            margin-bottom: var(--space-xl);
        }

        .lang-card {
            background: var(--bg-card);
            border: 2px solid transparent;
            border-radius: var(--radius-lg);
            padding: var(--space-lg);
            text-align: center;
            cursor: pointer;
            transition: all var(--transition-base);
            position: relative;
        }

        .lang-card:hover {
            transform: translateY(-4px);
            background: var(--bg-hover);
            box-shadow: var(--shadow-md);
        }

        .lang-card.selected {
            border-color: var(--secondary);
            background: rgba(255, 179, 0, 0.1);
            box-shadow: var(--shadow-glow);
        }

        .lang-card:focus-visible {
            outline: none;
            box-shadow: var(--focus-ring);
        }

        .lang-flag {
            font-size: 2.5rem;
            margin-bottom: var(--space-sm);
            display: block;
        }

        .lang-name {
            font-weight: 600;
            font-size: 1rem;
            margin-bottom: 2px;
        }

        .lang-native {
            font-size: 0.8rem;
            color: var(--text-muted);
        }

        .lang-check {
            position: absolute;
            top: 8px;
            right: 8px;
            width: 24px;
            height: 24px;
            background: var(--secondary);
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: #000;
            font-size: 0.8rem;
            opacity: 0;
            transform: scale(0);
            transition: all var(--transition-base);
        }

        .lang-card.selected .lang-check {
            opacity: 1;
            transform: scale(1);
        }

        /* Accessibility Profiles */
        .profile-grid {
            display: flex;
            flex-direction: column;
            gap: var(--space-md);
            margin-bottom: var(--space-xl);
        }

        .profile-card {
            display: flex;
            align-items: center;
            gap: var(--space-md);
            padding: var(--space-lg);
            background: var(--bg-card);
            border: 2px solid transparent;
            border-radius: var(--radius-lg);
            cursor: pointer;
            transition: all var(--transition-base);
        }

        .profile-card:hover {
            background: var(--bg-hover);
            transform: translateX(4px);
        }

        .profile-card.selected {
            border-color: var(--secondary);
            background: rgba(255, 179, 0, 0.1);
        }

        .profile-icon {
            width: 56px;
            height: 56px;
            border-radius: var(--radius-md);
            background: rgba(255,255,255,0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.75rem;
            flex-shrink: 0;
        }

        .profile-info h3 {
            font-size: 1.1rem;
            margin-bottom: 4px;
        }

        .profile-info p {
            font-size: 0.875rem;
            color: var(--text-secondary);
            line-height: 1.4;
        }

        .profile-badge {
            display: inline-block;
            padding: 2px 8px;
            background: var(--secondary);
            color: #000;
            font-size: 0.7rem;
            font-weight: 700;
            border-radius: 4px;
            margin-top: 4px;
            text-transform: uppercase;
        }

        /* Auth Method Selection */
        .auth-options {
            display: flex;
            flex-direction: column;
            gap: var(--space-md);
            margin-bottom: var(--space-xl);
        }

        .auth-card {
            display: flex;
            align-items: center;
            gap: var(--space-md);
            padding: var(--space-lg);
            background: var(--bg-card);
            border: 2px solid transparent;
            border-radius: var(--radius-lg);
            cursor: pointer;
            transition: all var(--transition-base);
        }

        .auth-card:hover {
            background: var(--bg-hover);
            border-color: rgba(255,255,255,0.2);
        }

        .auth-card.selected {
            border-color: var(--secondary);
            background: rgba(255, 179, 0, 0.1);
        }

        .auth-icon {
            width: 48px;
            height: 48px;
            border-radius: var(--radius-md);
            background: rgba(255,255,255,0.1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.5rem;
        }

        /* OTP Input */
        .otp-container {
            display: flex;
            justify-content: center;
            gap: var(--space-md);
            margin: var(--space-xl) 0;
        }

        .otp-input {
            width: 64px;
            height: 64px;
            text-align: center;
            font-size: 1.5rem;
            font-weight: 700;
            background: var(--bg-card);
            border: 2px solid rgba(255,255,255,0.2);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            transition: all var(--transition-base);
        }

        .otp-input:focus {
            outline: none;
            border-color: var(--secondary);
            box-shadow: var(--shadow-glow);
            transform: scale(1.05);
        }

        /* Progress Steps */
        .steps-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            margin-bottom: var(--space-xl);
            position: relative;
        }

        .step-line {
            position: absolute;
            top: 50%;
            left: 40px;
            right: 40px;
            height: 2px;
            background: rgba(255,255,255,0.1);
            z-index: 0;
        }

        .step {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            background: var(--bg-card);
            border: 2px solid rgba(255,255,255,0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 700;
            font-size: 0.875rem;
            z-index: 1;
            transition: all var(--transition-base);
        }

        .step.active {
            background: var(--secondary);
            border-color: var(--secondary);
            color: #000;
            box-shadow: var(--shadow-glow);
        }

        .step.completed {
            background: var(--success);
            border-color: var(--success);
            color: white;
        }

        /* Dashboard */
        .dashboard-header {
            display: flex;
            align-items: center;
            justify-content: space-between;
            padding: var(--space-md) 0;
            margin-bottom: var(--space-lg);
            border-bottom: 1px solid rgba(255,255,255,0.1);
        }

        .brand {
            display: flex;
            align-items: center;
            gap: var(--space-sm);
        }

        .brand-logo {
            width: 40px;
            height: 40px;
            background: linear-gradient(135deg, var(--secondary), var(--secondary-light));
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: 800;
            color: #000;
            font-size: 1.25rem;
        }

        .brand-text {
            font-size: 1.25rem;
            font-weight: 700;
        }

        .connection-status {
            display: flex;
            align-items: center;
            gap: 6px;
            padding: 6px 12px;
            background: rgba(0,0,0,0.3);
            border-radius: 20px;
            font-size: 0.75rem;
            font-weight: 500;
        }

        .status-dot {
            width: 8px;
            height: 8px;
            border-radius: 50%;
            animation: pulse 2s infinite;
        }

        .status-online { background: var(--success); }
        .status-mesh { background: var(--secondary); }
        .status-offline { background: var(--error); }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        /* Feature Grid */
        .feature-grid {
            display: grid;
            grid-template-columns: repeat(2, 1fr);
            gap: var(--space-md);
            margin-bottom: var(--space-lg);
        }

        .feature-card {
            background: var(--bg-card);
            border: 1px solid rgba(255,255,255,0.05);
            border-radius: var(--radius-lg);
            padding: var(--space-lg);
            text-align: center;
            cursor: pointer;
            transition: all var(--transition-base);
            position: relative;
            overflow: hidden;
        }

        .feature-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.1), transparent);
            transition: left 0.5s;
        }

        .feature-card:hover::before {
            left: 100%;
        }

        .feature-card:hover {
            transform: translateY(-4px);
            background: var(--bg-hover);
            box-shadow: var(--shadow-md);
            border-color: rgba(255,255,255,0.1);
        }

        .feature-icon {
            width: 56px;
            height: 56px;
            margin: 0 auto var(--space-sm);
            background: rgba(255,255,255,0.1);
            border-radius: var(--radius-md);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.75rem;
        }

        .feature-title {
            font-weight: 600;
            font-size: 0.9rem;
            margin-bottom: 4px;
        }

        .feature-desc {
            font-size: 0.75rem;
            color: var(--text-muted);
        }

        .feature-badge {
            position: absolute;
            top: 8px;
            right: 8px;
            padding: 2px 6px;
            background: var(--success);
            color: white;
            font-size: 0.65rem;
            font-weight: 700;
            border-radius: 4px;
            text-transform: uppercase;
        }

        /* Chat Interface */
        .chat-container {
            flex: 1;
            display: flex;
            flex-direction: column;
            background: var(--bg-card);
            border-radius: var(--radius-lg);
            overflow: hidden;
        }

        .chat-header {
            display: flex;
            align-items: center;
            gap: var(--space-md);
            padding: var(--space-md);
            background: rgba(0,0,0,0.2);
            border-bottom: 1px solid rgba(255,255,255,0.05);
        }

        .chat-avatar {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 1.25rem;
        }

        .chat-info h4 {
            font-size: 1rem;
            margin-bottom: 2px;
        }

        .chat-info span {
            font-size: 0.75rem;
            color: var(--success);
        }

        .chat-messages {
            flex: 1;
            overflow-y: auto;
            padding: var(--space-md);
            display: flex;
            flex-direction: column;
            gap: var(--space-md);
        }

        .message {
            max-width: 80%;
            padding: var(--space-md);
            border-radius: var(--radius-lg);
            position: relative;
            animation: messageSlide 0.3s ease;
        }

        @keyframes messageSlide {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        .message.sent {
            align-self: flex-end;
            background: linear-gradient(135deg, var(--accent), var(--accent-light));
            border-bottom-right-radius: 4px;
        }

        .message.received {
            align-self: flex-start;
            background: var(--bg-hover);
            border-bottom-left-radius: 4px;
        }

        .message-time {
            font-size: 0.7rem;
            color: rgba(255,255,255,0.6);
            margin-top: 4px;
            text-align: right;
        }

        .chat-input-area {
            display: flex;
            gap: var(--space-sm);
            padding: var(--space-md);
            background: rgba(0,0,0,0.2);
        }

        .chat-input {
            flex: 1;
            padding: var(--space-md);
            background: var(--bg-card);
            border: 1px solid rgba(255,255,255,0.1);
            border-radius: var(--radius-md);
            color: var(--text-primary);
            font-size: 1rem;
        }

        .chat-input:focus {
            outline: none;
            border-color: var(--secondary);
        }

        /* Voice Control Button */
        .voice-btn {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: var(--secondary);
            border: none;
            color: #000;
            font-size: 1.25rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all var(--transition-base);
        }

        .voice-btn:hover {
            transform: scale(1.1);
            box-shadow: var(--shadow-glow);
        }

        .voice-btn.recording {
            animation: recordingPulse 1.5s infinite;
        }

        @keyframes recordingPulse {
            0%, 100% { box-shadow: 0 0 0 0 rgba(255, 179, 0, 0.7); }
            50% { box-shadow: 0 0 0 20px rgba(255, 179, 0, 0); }
        }

        /* Sign Language Canvas */
        .sign-canvas {
            width: 100%;
            height: 300px;
            background: #000;
            border-radius: var(--radius-lg);
            position: relative;
            overflow: hidden;
            margin-bottom: var(--space-md);
        }

        .sign-overlay {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            padding: var(--space-md);
            background: linear-gradient(transparent, rgba(0,0,0,0.8));
        }

        .sign-text {
            font-size: 1.25rem;
            font-weight: 600;
            color: var(--secondary);
        }

        /* Toast Notifications */
        .toast-container {
            position: fixed;
            top: 20px;
            left: 50%;
            transform: translateX(-50%);
            z-index: 1000;
            display: flex;
            flex-direction: column;
            gap: var(--space-sm);
            pointer-events: none;
        }

        .toast {
            padding: var(--space-md) var(--space-lg);
            background: rgba(0,0,0,0.9);
            border-left: 4px solid var(--secondary);
            border-radius: var(--radius-md);
            color: white;
            font-size: 0.9rem;
            animation: toastSlide 0.3s ease;
            pointer-events: auto;
            max-width: 90vw;
        }

        @keyframes toastSlide {
            from { transform: translateY(-100%); opacity: 0; }
            to { transform: translateY(0); opacity: 1; }
        }

        /* Modal */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.8);
            display: flex;
            align-items: center;
            justify-content: center;
            z-index: 1000;
            opacity: 0;
            visibility: hidden;
            transition: all var(--transition-base);
        }

        .modal-overlay.active {
            opacity: 1;
            visibility: visible;
        }

        .modal {
            background: var(--bg-dark);
            border-radius: var(--radius-xl);
            padding: var(--space-xl);
            max-width: 90%;
            width: 400px;
            transform: scale(0.9);
            transition: transform var(--transition-base);
        }

        .modal-overlay.active .modal {
            transform: scale(1);
        }

        /* Accessibility Toolbar */
        .a11y-toolbar {
            position: fixed;
            bottom: 20px;
            right: 20px;
            display: flex;
            flex-direction: column;
            gap: var(--space-sm);
            z-index: 100;
        }

        .a11y-btn {
            width: 48px;
            height: 48px;
            border-radius: 50%;
            background: var(--bg-card);
            border: 1px solid rgba(255,255,255,0.2);
            color: var(--text-primary);
            font-size: 1.25rem;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            transition: all var(--transition-base);
            box-shadow: var(--shadow-md);
        }

        .a11y-btn:hover {
            background: var(--secondary);
            color: #000;
            transform: scale(1.1);
        }

        /* Skip Link */
        .skip-link {
            position: absolute;
            top: -40px;
            left: 0;
            padding: 8px;
            background: var(--secondary);
            color: #000;
            font-weight: 600;
            z-index: 10000;
            transition: top var(--transition-base);
        }

        .skip-link:focus {
            top: 0;
        }

        /* Loading Spinner */
        .spinner {
            width: 40px;
            height: 40px;
            border: 3px solid rgba(255,255,255,0.1);
            border-top-color: var(--secondary);
            border-radius: 50%;
            animation: spin 1s linear infinite;
        }

        @keyframes spin {
            to { transform: rotate(360deg); }
        }

        /* Responsive */
        @media (max-width: 480px) {
            #app {
                border-radius: 0;
                min-height: 100vh;
                margin: 0;
            }
            
            .lang-grid {
                grid-template-columns: 1fr;
            }
            
            .feature-grid {
                grid-template-columns: 1fr;
            }
        }

        /* Reduced Motion */
        @media (prefers-reduced-motion: reduce) {
            * {
                animation-duration: 0.01ms !important;
                animation-iteration-count: 1 !important;
                transition-duration: 0.01ms !important;
            }
        }

        /* High Contrast Mode */
        @media (prefers-contrast: high) {
            :root {
                --bg-card: #000000;
                --text-primary: #ffffff;
                --primary: #00ff00;
                --secondary: #ffff00;
            }
        }

        /* Focus Visible Polyfill */
        .js-focus-visible :focus:not(.focus-visible) {
            outline: none;
        }
    </style>
</head>
<body>

    <!-- Skip to main content link for screen readers -->
    <a href="#main-content" class="skip-link">Skip to main content</a>

    <!-- Background -->
    <div class="bg-canvas"></div>
    <div class="bg-particles" id="particles"></div>

    <!-- Toast Container -->
    <div class="toast-container" id="toastContainer"></div>

    <!-- Main App -->
    <div id="app">
        
        <!-- SCREEN: WELCOME / LANGUAGE SELECTION -->
        <div id="screen-welcome" class="screen active">
            <div style="text-align: center; margin-top: 60px; margin-bottom: 40px;">
                <div class="brand-logo" style="width: 80px; height: 80px; margin: 0 auto 20px; font-size: 2.5rem;">J</div>
                <h1>JAMBO</h1>
                <p class="subtitle">Connect Beyond Limits</p>
            </div>

            <h2 style="font-size: 1.25rem; margin-bottom: 16px;">Select Your Language / Chagua Lugha</h2>
            
            <div class="lang-grid" role="radiogroup" aria-label="Select language">
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('en')" onkeypress="handleKeySelect(event, 'en')">
                    <span class="lang-flag">🇬🇧</span>
                    <div class="lang-name">English</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('sw')" onkeypress="handleKeySelect(event, 'sw')">
                    <span class="lang-flag">🇹🇿</span>
                    <div class="lang-name">Kiswahili</div>
                    <div class="lang-native">Lugha ya Taifa</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('fr')" onkeypress="handleKeySelect(event, 'fr')">
                    <span class="lang-flag">🇫🇷</span>
                    <div class="lang-name">Français</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('de')" onkeypress="handleKeySelect(event, 'de')">
                    <span class="lang-flag">🇩🇪</span>
                    <div class="lang-name">Deutsch</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('zu')" onkeypress="handleKeySelect(event, 'zu')">
                    <span class="lang-flag">🇿🇦</span>
                    <div class="lang-name">isiZulu</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('rw')" onkeypress="handleKeySelect(event, 'rw')">
                    <span class="lang-flag">🇷🇼</span>
                    <div class="lang-name">Kinyarwanda</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('ar')" onkeypress="handleKeySelect(event, 'ar')">
                    <span class="lang-flag">🇸🇦</span>
                    <div class="lang-name">العربية</div>
                    <div class="lang-native">Arabic</div>
                    <div class="lang-check">✓</div>
                </div>
                <div class="lang-card" role="radio" tabindex="0" aria-checked="false" onclick="selectLanguage('zh')" onkeypress="handleKeySelect(event, 'zh')">
                    <span class="lang-flag">🇨🇳</span>
                    <div class="lang-name">中文</div>
                    <div class="lang-native">Chinese</div>
                    <div class="lang-check">✓</div>
                </div>
            </div>

            <button class="btn btn-primary btn-block btn-lg" id="langContinue" onclick="goToAccessibility()" disabled>
                Continue <i class="fas fa-arrow-right"></i>
            </button>

            <p style="text-align: center; margin-top: 20px; font-size: 0.875rem; color: var(--text-muted);">
                <i class="fas fa-globe"></i> 50+ languages available in settings
            </p>
        </div>

        <!-- SCREEN: ACCESSIBILITY PROFILE -->
        <div id="screen-accessibility" class="screen">
            <button class="btn btn-ghost" onclick="goBack('screen-welcome')" style="width: auto; margin-bottom: 20px;">
                <i class="fas fa-arrow-left"></i> Back
            </button>

            <h2>Accessibility Profile</h2>
            <p class="subtitle">Customize your experience for maximum comfort and usability</p>

            <div class="profile-grid" role="radiogroup" aria-label="Select accessibility profile">
                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('standard')" onkeypress="handleKeySelect(event, 'standard', 'profile')">
                    <div class="profile-icon">👤</div>
                    <div class="profile-info">
                        <h3>Standard</h3>
                        <p>Default interface optimized for general use</p>
                    </div>
                </div>

                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('visual')" onkeypress="handleKeySelect(event, 'visual', 'profile')">
                    <div class="profile-icon">👁️</div>
                    <div class="profile-info">
                        <h3>Visual Support</h3>
                        <p>High contrast, large text, screen reader optimized</p>
                        <span class="profile-badge">WCAG AAA</span>
                    </div>
                </div>

                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('hearing')" onkeypress="handleKeySelect(event, 'hearing', 'profile')">
                    <div class="profile-icon">👂</div>
                    <div class="profile-info">
                        <h3>Hearing Support</h3>
                        <p>Visual alerts, captions, sign language integration</p>
                        <span class="profile-badge">AI Powered</span>
                    </div>
                </div>

                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('motor')" onkeypress="handleKeySelect(event, 'motor', 'profile')">
                    <div class="profile-icon">✋</div>
                    <div class="profile-info">
                        <h3>Motor Support</h3>
                        <p>Large touch targets, voice control, switch access</p>
                        <span class="profile-badge">Voice Ready</span>
                    </div>
                </div>

                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('cognitive')" onkeypress="handleKeySelect(event, 'cognitive', 'profile')">
                    <div class="profile-icon">🧠</div>
                    <div class="profile-info">
                        <h3>Cognitive Support</h3>
                        <p>Simplified interface, reading assistance, memory aids</p>
                    </div>
                </div>

                <div class="profile-card" role="radio" tabindex="0" aria-checked="false" onclick="selectProfile('deafblind')" onkeypress="handleKeySelect(event, 'deafblind', 'profile')">
                    <div class="profile-icon">🤲</div>
                    <div class="profile-info">
                        <h3>Deafblind Support</h3>
                        <p>Braille display, haptic feedback, tactile signing</p>
                        <span class="profile-badge">Advanced</span>
                    </div>
                </div>
            </div>

            <button class="btn btn-primary btn-block btn-lg" id="profileContinue" onclick="goToAuthMethod()" disabled>
                Continue <i class="fas fa-arrow-right"></i>
            </button>
        </div>

        <!-- SCREEN: AUTHENTICATION METHOD -->
        <div id="screen-auth-method" class="screen">
            <div class="steps-header">
                <div class="step-line"></div>
                <div class="step completed">1</div>
                <div class="step completed">2</div>
                <div class="step active">3</div>
                <div class="step">4</div>
            </div>

            <h2>How would you like to sign in?</h2>

            <div class="auth-options" role="radiogroup" aria-label="Select authentication method">
                <div class="auth-card" role="radio" tabindex="0" aria-checked="false" onclick="selectAuthMethod('phone')" onkeypress="handleKeySelect(event, 'phone', 'auth')">
                    <div class="auth-icon" style="background: rgba(59, 130, 246, 0.2); color: #60a5fa;">
                        <i class="fas fa-mobile-alt"></i>
                    </div>
                    <div class="profile-info">
                        <h3>Phone Number</h3>
                        <p>SMS verification to your mobile number</p>
                    </div>
                </div>

                <div class="auth-card" role="radio" tabindex="0" aria-checked="false" onclick="selectAuthMethod('email')" onkeypress="handleKeySelect(event, 'email', 'auth')">
                    <div class="auth-icon" style="background: rgba(16, 185, 129, 0.2); color: #34d399;">
                        <i class="fas fa-envelope"></i>
                    </div>
                    <div class="profile-info">
                        <h3>Email Address</h3>
                        <p>Verification link or code to your email</p>
                    </div>
                </div>

                <div class="auth-card" role="radio" tabindex="0" aria-checked="false" onclick="selectAuthMethod('social')" onkeypress="handleKeySelect(event, 'social', 'auth')">
                    <div class="auth-icon" style="background: rgba(139, 92, 246, 0.2); color: #a78bfa;">
                        <i class="fas fa-user-friends"></i>
                    </div>
                    <div class="profile-info">
                        <h3>Social Account</h3>
                        <p>Google, Microsoft, or Apple account</p>
                    </div>
                </div>
            </div>

            <button class="btn btn-primary btn-block btn-lg" id="authContinue" onclick="goToCredentials()" disabled>
                Continue <i class="fas fa-arrow-right"></i>
            </button>
        </div>

        <!-- SCREEN: CREDENTIALS INPUT -->
        <div id="screen-credentials" class="screen">
            <div class="steps-header">
                <div class="step-line"></div>
                <div class="step completed">1</div>
                <div class="step completed">2</div>
                <div class="step completed">3</div>
                <div class="step active">4</div>
            </div>

            <h2 id="credTitle">Enter Your Details</h2>

            <!-- Phone Input -->
            <div id="phone-input-section">
                <div class="input-group">
                    <label class="input-label">Phone Number</label>
                    <div class="phone-input-wrapper">
                        <select class="country-select" id="countryCode" aria-label="Country code">
                            <!-- Populated by JS -->
                        </select>
                        <input type="tel" class="input-field" id="phoneNumber" placeholder="712 345 678" aria-label="Phone number">
                    </div>
                    <span class="error-message" id="phoneError" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> Please enter a valid phone number
                    </span>
                </div>
            </div>

            <!-- Email Input -->
            <div id="email-input-section" style="display: none;">
                <div class="input-group">
                    <label class="input-label">Email Address</label>
                    <input type="email" class="input-field" id="emailAddress" placeholder="your.name@example.com" aria-label="Email address">
                    <span class="error-message" id="emailError" style="display: none;">
                        <i class="fas fa-exclamation-circle"></i> Please enter a valid email address
                    </span>
                </div>
            </div>

            <!-- Social Login -->
            <div id="social-login-section" style="display: none;">
                <p class="subtitle">Choose your provider:</p>
                <button class="btn btn-secondary btn-block" style="margin-bottom: 12px;">
                    <i class="fab fa-google" style="color: #ea4335;"></i> Continue with Google
                </button>
                <button class="btn btn-secondary btn-block" style="margin-bottom: 12px;">
                    <i class="fab fa-microsoft" style="color: #00a4ef;"></i> Continue with Microsoft
                </button>
                <button class="btn btn-secondary btn-block">
                    <i class="fab fa-apple" style="color: #fff;"></i> Continue with Apple
                </button>
            </div>

            <button class="btn btn-primary btn-block btn-lg" id="sendCodeBtn" onclick="sendVerification()">
                Send Verification Code <i class="fas fa-paper-plane"></i>
            </button>

            <button class="btn btn-ghost btn-block" onclick="goBack('screen-auth-method')">
                <i class="fas fa-arrow-left"></i> Choose Different Method
            </button>
        </div>

        <!-- SCREEN: VERIFICATION -->
        <div id="screen-verification" class="screen">
            <h2>Verify Your Identity</h2>
            <p class="subtitle" id="verifySubtitle">Enter the 6-digit code sent to your phone</p>

            <div class="otp-container" role="group" aria-label="Verification code">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 1" onkeyup="handleOtpInput(this, 0)">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 2" onkeyup="handleOtpInput(this, 1)">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 3" onkeyup="handleOtpInput(this, 2)">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 4" onkeyup="handleOtpInput(this, 3)">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 5" onkeyup="handleOtpInput(this, 4)">
                <input type="text" class="otp-input" maxlength="1" aria-label="Digit 6" onkeyup="handleOtpInput(this, 5)">
            </div>

            <button class="btn btn-primary btn-block btn-lg" onclick="verifyCode()">
                Verify <i class="fas fa-check"></i>
            </button>

            <p style="text-align: center; margin-top: 20px; color: var(--text-secondary);">
                Didn't receive it? <a href="#" onclick="resendCode()" style="color: var(--secondary);">Resend code</a>
            </p>

            <button class="btn btn-ghost btn-block" onclick="goBack('screen-credentials')">
                <i class="fas fa-arrow-left"></i> Back
            </button>
        </div>

        <!-- SCREEN: DASHBOARD -->
        <div id="screen-dashboard" class="screen">
            <div class="dashboard-header">
                <div class="brand">
                    <div class="brand-logo">J</div>
                    <div>
                        <div class="brand-text">JAMBO</div>
                        <div style="font-size: 0.75rem; color: var(--text-muted);">v2.0</div>
                    </div>
                </div>
                <div class="connection-status status-mesh">
                    <span class="status-dot"></span>
                    <span>Mesh Active</span>
                </div>
            </div>

            <!-- Quick Actions -->
            <div class="feature-grid">
                <div class="feature-card" onclick="openChat()">
                    <div class="feature-icon" style="background: rgba(59, 130, 246, 0.2); color: #60a5fa;">
                        <i class="fas fa-comment-dots"></i>
                    </div>
                    <div class="feature-title">Messages</div>
                    <div class="feature-desc">Chat via phone or email</div>
                    <span class="feature-badge">3 New</span>
                </div>

                <div class="feature-card" onclick="openSignTranslate()">
                    <div class="feature-icon" style="background: rgba(236, 72, 153, 0.2); color: #f472b6;">
                        <i class="fas fa-sign-language"></i>
                    </div>
                    <div class="feature-title">Sign Translate</div>
                    <div class="feature-desc">AI-powered recognition</div>
                </div>

                <div class="feature-card" onclick="triggerEmergency()">
                    <div class="feature-icon" style="background: rgba(239, 68, 68, 0.2); color: #f87171;">
                        <i class="fas fa-exclamation-triangle"></i>
                    </div>
                    <div class="feature-title">Emergency</div>
                    <div class="feature-desc">Instant alert broadcast</div>
                </div>

                <div class="feature-card" onclick="openNetworkMap()">
                    <div class="feature-icon" style="background: rgba(16, 185, 129, 0.2); color: #34d399;">
                        <i class="fas fa-network-wired"></i>
                    </div>
                    <div class="feature-title">Mesh Network</div>
                    <div class="feature-desc">12 peers nearby</div>
                    <span class="feature-badge">Live</span>
                </div>

                <div class="feature-card" onclick="openVoiceControl()">
                    <div class="feature-icon" style="background: rgba(139, 92, 246, 0.2); color: #a78bfa;">
                        <i class="fas fa-microphone"></i>
                    </div>
                    <div class="feature-title">Voice Control</div>
                    <div class="feature-desc">Hands-free navigation</div>
                </div>

                <div class="feature-card" onclick="openSettings()">
                    <div class="feature-icon" style="background: rgba(107, 114, 128, 0.2); color: #9ca3af;">
                        <i class="fas fa-cog"></i>
                    </div>
                    <div class="feature-title">Settings</div>
                    <div class="feature-desc">Customize your experience</div>
                </div>
            </div>

            <!-- Recent Activity -->
            <div style="margin-top: auto; padding: 20px; background: var(--bg-card); border-radius: var(--radius-lg);">
                <h3 style="font-size: 1rem; margin-bottom: 12px; color: var(--secondary);">
                    <i class="fas fa-bolt"></i> Quick Tip
                </h3>
                <p style="font-size: 0.9rem; color: var(--text-secondary);">
                    Say "Hey Jambo" or press <kbd style="background: rgba(255,255,255,0.1); padding: 2px 6px; border-radius: 4px;">Space</kbd> to start voice control
                </p>
            </div>
        </div>

        <!-- SCREEN: CHAT -->
        <div id="screen-chat" class="screen">
            <div class="chat-container">
                <div class="chat-header">
                    <button class="btn btn-ghost" onclick="showScreen('screen-dashboard')" style="width: auto; padding: 8px;">
                        <i class="fas fa-arrow-left"></i>
                    </button>
                    <div class="chat-avatar">
                        <i class="fas fa-user"></i>
                    </div>
                    <div class="chat-info" style="flex: 1;">
                        <h4>John Doe</h4>
                        <span>Online • Mesh Network</span>
                    </div>
                    <button class="btn btn-ghost" style="width: auto; padding: 8px;">
                        <i class="fas fa-phone"></i>
                    </button>
                    <button class="btn btn-ghost" style="width: auto; padding: 8px;">
                        <i class="fas fa-video"></i>
                    </button>
                </div>

                <div class="chat-messages" id="chatMessages">
                    <div class="message received">
                        Hello! How are you doing today?
                        <div class="message-time">10:30 AM</div>
                    </div>
                </div>

                <div class="chat-input-area">
                    <button class="btn btn-ghost voice-btn" id="voiceBtn" onclick="toggleVoiceInput()" aria-label="Voice input">
                        <i class="fas fa-microphone"></i>
                    </button>
                    <input type="text" class="chat-input" id="messageInput" placeholder="Type a message..." aria-label="Message input">
                    <button class="btn btn-primary" style="width: auto; padding: 12px 20px;" onclick="sendMessage()">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- SCREEN: SIGN TRANSLATE -->
        <div id="screen-sign" class="screen">
            <div class="dashboard-header">
                <button class="btn btn-ghost" onclick="showScreen('screen-dashboard')" style="width: auto;">
                    <i class="fas fa-arrow-left"></i>
                </button>
                <h2 style="margin: 0;">Sign Language Translator</h2>
                <div style="width: 40px;"></div>
            </div>

            <div class="sign-canvas">
                <video id="signVideo" autoplay playsinline style="width: 100%; height: 100%; object-fit: cover;"></video>
                <div class="sign-overlay">
                    <div class="sign-text" id="signText">Waiting for signs...</div>
                </div>
            </div>

            <div style="display: flex; gap: 12px; margin-bottom: 16px;">
                <button class="btn btn-primary" style="flex: 1;" onclick="startCamera()">
                    <i class="fas fa-camera"></i> Start Camera
                </button>
                <button class="btn btn-secondary" style="flex: 1;" onclick="switchCamera()">
                    <i class="fas fa-sync"></i> Switch
                </button>
            </div>

            <div style="background: var(--bg-card); padding: 16px; border-radius: var(--radius-lg);">
                <h4 style="margin-bottom: 8px; color: var(--secondary);">Supported Signs</h4>
                <p style="font-size: 0.875rem; color: var(--text-secondary);">
                    Hello • Thank You • Help • Water • Food • Friend • Yes • No • Emergency
                </p>
            </div>
        </div>

    </div>

    <!-- Accessibility Toolbar -->
    <div class="a11y-toolbar">
        <button class="a11y-btn" onclick="toggleHighContrast()" title="Toggle high contrast" aria-label="Toggle high contrast">
            <i class="fas fa-adjust"></i>
        </button>
        <button class="a11y-btn" onclick="toggleLargeText()" title="Toggle large text" aria-label="Toggle large text">
            <i class="fas fa-font"></i>
        </button>
        <button class="a11y-btn" onclick="startVoiceControl()" title="Voice control" aria-label="Start voice control">
            <i class="fas fa-microphone"></i>
        </button>
    </div>

    <script>
        // ==================== DATA & CONFIG ====================
        const countries = [
            { code: "+255", flag: "🇹🇿", name: "Tanzania" },
            { code: "+254", flag: "🇰🇪", name: "Kenya" },
            { code: "+256", flag: "🇺🇬", name: "Uganda" },
            { code: "+250", flag: "🇷🇼", name: "Rwanda" },
            { code: "+27", flag: "🇿🇦", name: "South Africa" },
            { code: "+1", flag: "🇺🇸", name: "USA" },
            { code: "+44", flag: "🇬🇧", name: "UK" },
            { code: "+49", flag: "🇩🇪", name: "Germany" },
            { code: "+33", flag: "🇫🇷", name: "France" },
            { code: "+91", flag: "🇮🇳", name: "India" },
            { code: "+86", flag: "🇨🇳", name: "China" },
            { code: "+234", flag: "🇳🇬", name: "Nigeria" },
            { code: "+20", flag: "🇪🇬", name: "Egypt" },
            { code: "+966", flag: "🇸🇦", name: "Saudi Arabia" },
            { code: "+971", flag: "🇦🇪", name: "UAE" }
        ];

        const translations = {
            en: {
                welcome: "Welcome",
                selectLanguage: "Select Your Language",
                accessibility: "Accessibility Profile",
                continue: "Continue",
                phoneNumber: "Phone Number",
                emailAddress: "Email Address",
                verifyCode: "Verify Code",
                enterCode: "Enter the 6-digit code",
                resendCode: "Resend code",
                messages: "Messages",
                signTranslate: "Sign Translate",
                emergency: "Emergency",
                network: "Mesh Network",
                settings: "Settings"
            },
            sw: {
                welcome: "Karibu",
                selectLanguage: "Chagua Lugha Yako",
                accessibility: "Wasifu wa Ufikiaji",
                continue: "Endelea",
                phoneNumber: "Nambari ya Simu",
                emailAddress: "Barua Pepe",
                verifyCode: "Thibitisha Nambari",
                enterCode: "Weka nambari ya tarakimu 6",
                resendCode: "Tuma tena",
                messages: "Ujumbe",
                signTranslate: "Tafsiri ya Ishara",
                emergency: "Dharura",
                network: "Mtandao wa Mesh",
                settings: "Mipangilio"
            },
            fr: {
                welcome: "Bienvenue",
                selectLanguage: "Choisissez votre langue",
                accessibility: "Profil d'accessibilité",
                continue: "Continuer",
                phoneNumber: "Numéro de téléphone",
                emailAddress: "Adresse e-mail",
                verifyCode: "Vérifier le code",
                enterCode: "Entrez le code à 6 chiffres",
                resendCode: "Renvoyer le code",
                messages: "Messages",
                signTranslate: "Traduction des signes",
                emergency: "Urgence",
                network: "Réseau Mesh",
                settings: "Paramètres"
            },
            de: {
                welcome: "Willkommen",
                selectLanguage: "Wähle deine Sprache",
                accessibility: "Barrierefreiheitsprofil",
                continue: "Weiter",
                phoneNumber: "Telefonnummer",
                emailAddress: "E-Mail-Adresse",
                verifyCode: "Code überprüfen",
                enterCode: "Geben Sie den 6-stelligen Code ein",
                resendCode: "Code erneut senden",
                messages: "Nachrichten",
                signTranslate: "Gebärdensprache",
                emergency: "Notfall",
                network: "Mesh-Netzwerk",
                settings: "Einstellungen"
            }
        };

        // ==================== STATE ====================
        let currentState = {
            language: 'en',
            profile: null,
            authMethod: null,
            phoneNumber: '',
            email: '',
            verificationCode: '',
            isVoiceActive: false,
            isHighContrast: false,
            isLargeText: false
        };

        // ==================== INITIALIZATION ====================
        document.addEventListener('DOMContentLoaded', () => {
            populateCountryCodes();
            createParticles();
            setupKeyboardNavigation();
            setupVoiceRecognition();
        });

        // ==================== NAVIGATION ====================
        function showScreen(screenId) {
            document.querySelectorAll('.screen').forEach(s => {
                s.classList.remove('active');
                s.setAttribute('aria-hidden', 'true');
            });
            const target = document.getElementById(screenId);
            target.classList.add('active');
            target.setAttribute('aria-hidden', 'false');
            target.focus();
        }

        function goBack(screenId) {
            showScreen(screenId);
        }

        // ==================== LANGUAGE SELECTION ====================
        function selectLanguage(lang) {
            currentState.language = lang;
            
            // Update UI
            document.querySelectorAll('.lang-card').forEach(card => {
                card.classList.remove('selected');
                card.setAttribute('aria-checked', 'false');
            });
            
            event.currentTarget.classList.add('selected');
            event.currentTarget.setAttribute('aria-checked', 'true');
            
            // Enable continue button
            document.getElementById('langContinue').disabled = false;
            
            // Apply language
            applyLanguage(lang);
            
            // Announce to screen readers
            announceToScreenReader(`Selected ${lang}`);
        }

        function applyLanguage(lang) {
            const texts = translations[lang];
            if (!texts) return;
            
            // Update document language
            document.documentElement.lang = lang;
            
            // Apply RTL for Arabic
            if (lang === 'ar') {
                document.body.dir = 'rtl';
            } else {
                document.body.dir = 'ltr';
            }
        }

        function goToAccessibility() {
            showScreen('screen-accessibility');
        }

        // ==================== ACCESSIBILITY PROFILE ====================
        function selectProfile(profile) {
            currentState.profile = profile;
            
            document.querySelectorAll('.profile-card').forEach(card => {
                card.classList.remove('selected');
                card.setAttribute('aria-checked', 'false');
            });
            
            event.currentTarget.classList.add('selected');
            event.currentTarget.setAttribute('aria-checked', 'true');
            
            document.getElementById('profileContinue').disabled = false;
            
            // Apply profile settings immediately
            applyProfileSettings(profile);
        }

        function applyProfileSettings(profile) {
            document.body.classList.remove('dyslexia-mode', 'high-contrast', 'large-text', 'reduce-motion');
            
            switch(profile) {
                case 'visual':
                    document.body.classList.add('high-contrast', 'large-text');
                    break;
                case 'cognitive':
                    document.body.classList.add('dyslexia-mode', 'large-text');
                    break;
                case 'motor':
                    // Increase touch targets
                    document.querySelectorAll('.btn, .feature-card, .lang-card').forEach(el => {
                        el.style.minHeight = '56px';
                    });
                    break;
                case 'deafblind':
                    // Enable haptic feedback
                    if ('vibrate' in navigator) {
                        navigator.vibrate(200);
                    }
                    break;
            }
        }

        function goToAuthMethod() {
            showScreen('screen-auth-method');
        }

        // ==================== AUTHENTICATION ====================
        function selectAuthMethod(method) {
            currentState.authMethod = method;
            
            document.querySelectorAll('.auth-card').forEach(card => {
                card.classList.remove('selected');
                card.setAttribute('aria-checked', 'false');
            });
            
            event.currentTarget.classList.add('selected');
            event.currentTarget.setAttribute('aria-checked', 'true');
            
            document.getElementById('authContinue').disabled = false;
        }

        function goToCredentials() {
            showScreen('screen-credentials');
            
            // Show appropriate input section
            document.getElementById('phone-input-section').style.display = 'none';
            document.getElementById('email-input-section').style.display = 'none';
            document.getElementById('social-login-section').style.display = 'none';
            
            switch(currentState.authMethod) {
                case 'phone':
                    document.getElementById('phone-input-section').style.display = 'block';
                    document.getElementById('credTitle').textContent = 'Enter Phone Number';
                    break;
                case 'email':
                    document.getElementById('email-input-section').style.display = 'block';
                    document.getElementById('credTitle').textContent = 'Enter Email Address';
                    break;
                case 'social':
                    document.getElementById('social-login-section').style.display = 'block';
                    document.getElementById('credTitle').textContent = 'Social Login';
                    document.getElementById('sendCodeBtn').style.display = 'none';
                    break;
            }
        }

        function populateCountryCodes() {
            const select = document.getElementById('countryCode');
            countries.forEach(country => {
                const option = document.createElement('option');
                option.value = country.code;
                option.textContent = `${country.flag} ${country.code}`;
                select.appendChild(option);
            });
        }

        // ==================== VERIFICATION ====================
        function sendVerification() {
            let isValid = false;
            
            if (currentState.authMethod === 'phone') {
                const phone = document.getElementById('phoneNumber').value;
                isValid = phone.length >= 9;
                if (!isValid) {
                    document.getElementById('phoneError').style.display = 'flex';
                    document.getElementById('phoneNumber').classList.add('input-error');
                } else {
                    currentState.phoneNumber = document.getElementById('countryCode').value + phone;
                    document.getElementById('verifySubtitle').textContent = 
                        `Enter the 6-digit code sent to ${currentState.phoneNumber}`;
                }
            } else if (currentState.authMethod === 'email') {
                const email = document.getElementById('emailAddress').value;
                isValid = email.includes('@') && email.includes('.');
                if (!isValid) {
                    document.getElementById('emailError').style.display = 'flex';
                    document.getElementById('emailAddress').classList.add('input-error');
                } else {
                    currentState.email = email;
                    document.getElementById('verifySubtitle').textContent = 
                        `Enter the 6-digit code sent to ${email}`;
                }
            }
            
            if (isValid) {
                showScreen('screen-verification');
                // Auto-focus first OTP input
                setTimeout(() => {
                    document.querySelector('.otp-input').focus();
                }, 100);
            }
        }

        function handleOtpInput(input, index) {
            if (input.value.length === 1) {
                const inputs = document.querySelectorAll('.otp-input');
                if (index < inputs.length - 1) {
                    inputs[index + 1].focus();
                } else {
                    // Auto-submit on last digit
                    verifyCode();
                }
            }
        }

        function verifyCode() {
            const inputs = document.querySelectorAll('.otp-input');
            const code = Array.from(inputs).map(i => i.value).join('');
            
            if (code.length === 6) {
                currentState.verificationCode = code;
                showToast('Verification successful!');
                showScreen('screen-dashboard');
                
                // Update user display
                const userDisplay = currentState.phoneNumber || currentState.email || 'User';
                document.getElementById('user-display').textContent = userDisplay;
            } else {
                showToast('Please enter all 6 digits');
            }
        }

        function resendCode() {
            showToast('New code sent!');
        }

        // ==================== DASHBOARD FEATURES ====================
        function openChat() {
            showScreen('screen-chat');
            // Focus input for accessibility
            setTimeout(() => {
                document.getElementById('messageInput').focus();
            }, 100);
        }

        function sendMessage() {
            const input = document.getElementById('messageInput');
            const text = input.value.trim();
            
            if (!text) return;
            
            const container = document.getElementById('chatMessages');
            const time = new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' });
            
            // Add sent message
            const msg = document.createElement('div');
            msg.className = 'message sent';
            msg.innerHTML = `
                ${escapeHtml(text)}
                <div class="message-time">${time}</div>
            `;
            container.appendChild(msg);
            
            // Clear input
            input.value = '';
            container.scrollTop = container.scrollHeight;
            
            // Simulate reply
            setTimeout(() => {
                const reply = document.createElement('div');
                reply.className = 'message received';
                reply.innerHTML = `
                    Thanks for your message! This is an automated reply via mesh network.
                    <div class="message-time">${new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' })}</div>
                `;
                container.appendChild(reply);
                container.scrollTop = container.scrollHeight;
                
                // Haptic feedback
                if ('vibrate' in navigator) {
                    navigator.vibrate(50);
                }
            }, 1000);
        }

        function openSignTranslate() {
            showScreen('screen-sign');
        }

        async function startCamera() {
            try {
                const stream = await navigator.mediaDevices.getUserMedia({ 
                    video: { facingMode: 'user' } 
                });
                document.getElementById('signVideo').srcObject = stream;
                document.getElementById('signText').textContent = 'Camera active - show signs';
            } catch (err) {
                showToast('Camera access denied. Please enable permissions.');
            }
        }

        function switchCamera() {
            // Toggle between front/back camera
            showToast('Switching camera...');
        }

        function triggerEmergency() {
            if (confirm('⚠️ Send emergency alert to all nearby devices?')) {
                // Broadcast via mesh network
                if ('vibrate' in navigator) {
                    navigator.vibrate([500, 200, 500, 200, 500]);
                }
                showToast('🚨 Emergency alert broadcasted!');
            }
        }

        function openNetworkMap() {
            showToast('Network map: 12 peers within 200m range');
        }

        function openVoiceControl() {
            startVoiceControl();
        }

        function openSettings() {
            showToast('Settings - Full language list: 50+ languages available');
        }

        // ==================== VOICE CONTROL ====================
        let recognition = null;
        
        function setupVoiceRecognition() {
            if ('webkitSpeechRecognition' in window || 'SpeechRecognition' in window) {
                const SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
                recognition = new SpeechRecognition();
                recognition.continuous = false;
                recognition.interimResults = true;
                recognition.lang = currentState.language === 'sw' ? 'sw-TZ' : 'en-US';
                
                recognition.onresult = (event) => {
                    const transcript = Array.from(event.results)
                        .map(result => result[0])
                        .map(result => result.transcript)
                        .join('');
                    
                    // Fill active input
                    const activeInput = document.activeElement;
                    if (activeInput.tagName === 'INPUT') {
                        activeInput.value = transcript;
                    }
                };
                
                recognition.onerror = (event) => {
                    console.error('Speech recognition error:', event.error);
                    document.getElementById('voiceBtn').classList.remove('recording');
                };
                
                recognition.onend = () => {
                    document.getElementById('voiceBtn').classList.remove('recording');
                };
            }
        }

        function toggleVoiceInput() {
            const btn = document.getElementById('voiceBtn');
            
            if (!recognition) {
                showToast('Voice recognition not supported in this browser');
                return;
            }
            
            if (btn.classList.contains('recording')) {
                recognition.stop();
                btn.classList.remove('recording');
            } else {
                recognition.start();
                btn.classList.add('recording');
                showToast('Listening... Speak now');
            }
        }

        function startVoiceControl() {
            showToast('Voice control activated. Say "Hey Jambo" followed by a command.');
        }

        // ==================== ACCESSIBILITY TOGGLES ====================
        function toggleHighContrast() {
            currentState.isHighContrast = !currentState.isHighContrast;
            document.body.classList.toggle('high-contrast', currentState.isHighContrast);
            showToast(currentState.isHighContrast ? 'High contrast enabled' : 'High contrast disabled');
        }

        function toggleLargeText() {
            currentState.isLargeText = !currentState.isLargeText;
            document.body.classList.toggle('large-text', currentState.isLargeText);
            showToast(currentState.isLargeText ? 'Large text enabled' : 'Large text disabled');
        }

        // ==================== KEYBOARD NAVIGATION ====================
        function setupKeyboardNavigation() {
            document.addEventListener('keydown', (e) => {
                // Space for voice control
                if (e.code === 'Space' && e.target.tagName !== 'INPUT') {
                    e.preventDefault();
                    startVoiceControl();
                }
                
                // Escape to go back
                if (e.code === 'Escape') {
                    const activeScreen = document.querySelector('.screen.active');
                    if (activeScreen.id !== 'screen-dashboard' && activeScreen.id !== 'screen-welcome') {
                        history.back();
                    }
                }
                
                // Arrow key navigation for cards
                if (['ArrowUp', 'ArrowDown', 'ArrowLeft', 'ArrowRight'].includes(e.key)) {
                    handleArrowNavigation(e);
                }
            });
        }

        function handleArrowNavigation(e) {
            const focusable = document.querySelectorAll('.screen.active [tabindex="0"], .screen.active button, .screen.active input');
            const current = document.activeElement;
            const index = Array.from(focusable).indexOf(current);
            
            let nextIndex;
            if (e.key === 'ArrowDown' || e.key === 'ArrowRight') {
                nextIndex = (index + 1) % focusable.length;
            } else {
                nextIndex = (index - 1 + focusable.length) % focusable.length;
            }
            
            focusable[nextIndex]?.focus();
            e.preventDefault();
        }

        function handleKeySelect(event, value, type) {
            if (event.key === 'Enter' || event.key === ' ') {
                event.preventDefault();
                if (type === 'profile') {
                    selectProfile(value);
                } else if (type === 'auth') {
                    selectAuthMethod(value);
                } else {
                    selectLanguage(value);
                }
            }
        }

        // ==================== UTILITIES ====================
        function showToast(message) {
            const container = document.getElementById('toastContainer');
            const toast = document.createElement('div');
            toast.className = 'toast';
            toast.textContent = message;
            toast.setAttribute('role', 'alert');
            toast.setAttribute('aria-live', 'polite');
            
            container.appendChild(toast);
            
            setTimeout(() => {
                toast.remove();
            }, 3000);
        }

        function announceToScreenReader(message) {
            const announcer = document.createElement('div');
            announcer.setAttribute('aria-live', 'assertive');
            announcer.setAttribute('aria-atomic', 'true');
            announcer.className = 'sr-only';
            announcer.style.position = 'absolute';
            announcer.style.left = '-10000px';
            announcer.textContent = message;
            
            document.body.appendChild(announcer);
            setTimeout(() => announcer.remove(), 1000);
        }

        function escapeHtml(text) {
            const div = document.createElement('div');
            div.textContent = text;
            return div.innerHTML;
        }

        function createParticles() {
            const container = document.getElementById('particles');
            for (let i = 0; i < 15; i++) {
                const p = document.createElement('div');
                p.className = 'particle';
                p.style.left = Math.random() * 100 + '%';
                p.style.width = p.style.height = (Math.random() * 6 + 2) + 'px';
                p.style.animationDuration = (Math.random() * 10 + 10) + 's';
                p.style.animationDelay = (Math.random() * 5) + 's';
                container.appendChild(p);
            }
        }

        // ==================== SERVICE WORKER ====================
        if ('serviceWorker' in navigator) {
            navigator.serviceWorker.register('/sw.js')
                .then(reg => console.log('SW registered:', reg))
                .catch(err => console.log('SW registration failed:', err));
        }
    </script>
</body>
</html>
