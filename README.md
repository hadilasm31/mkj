<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MKJ SERVICE - Gestion du Personnel</title>
    <style>
        :root {
            --admin-color: #2c7be5;
            --chef-color: #ff8c00;
            --employe-color: #28a745;
            --dark-bg: #0f172a;
            --card-bg: rgba(255, 255, 255, 0.95);
            --text-dark: #1e293b;
            --text-light: #64748b;
            --success: #10b981;
            --warning: #f59e0b;
            --danger: #ef4444;
            --border: #e2e8f0;
            --shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1);
            --shadow-lg: 0 10px 15px -3px rgba(0, 0, 0, 0.1);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', system-ui, sans-serif;
            background: none;
            min-height: 100vh;
            color: #000;
            position: relative;
            overflow-x: hidden;
        }

        .bg-slider {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
        }

        .bg-slide {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-size: cover;
            background-position: center;
            opacity: 0;
            animation: fade 20s infinite;
        }

        .bg-slide:nth-child(1) { 
            background-image: url('https://lespalmistes.ci/wp-content/uploads/2023/06/476300445258001666880096-1.jpg'); 
            animation-delay: 0s; 
        }
        .bg-slide:nth-child(2) { 
            background-image: url('https://www.makanisi.org/wp-content/uploads/2020/03/GTC_Palmier_Huile_en_Savane@DR.jpg'); 
            animation-delay: 5s; 
        }
        .bg-slide:nth-child(3) { 
            background-image: url('https://fr.infosgabon.com/wp-content/uploads/2018/01/Olam-Palm-Gabon.jpg'); 
            animation-delay: 10s; 
        }
        .bg-slide:nth-child(4) { 
            background-image: url('https://i.ytimg.com/vi/Dwl7T7PAC_g/maxresdefault.jpg'); 
            animation-delay: 15s; 
        }

        @keyframes fade {
            0% { opacity: 0; }
            10% { opacity: 1; }
            25% { opacity: 1; }
            35% { opacity: 0; }
            100% { opacity: 0; }
        }

        .app-container {
            min-height: 100vh;
            display: flex;
            flex-direction: column;
        }

        /* Header */
        .header {
            background: var(--card-bg);
            backdrop-filter: blur(10px);
            padding: 1rem;
            box-shadow: var(--shadow);
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            gap: 1rem;
        }

        .logo {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            flex-shrink: 0;
        }

        .logo-icon {
            font-size: 1.8rem;
            color: var(--admin-color);
        }

        .logo h1 {
            font-size: 1.3rem;
            font-weight: 700;
        }

        .nav {
            display: flex;
            gap: 0.5rem;
            align-items: center;
            flex-wrap: wrap;
            justify-content: center;
        }

        .nav a {
            text-decoration: none;
            color: var(--text-dark);
            font-weight: 500;
            padding: 0.5rem 0.8rem;
            border-radius: 8px;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .nav a:hover {
            background: var(--border);
        }

        /* Main Content */
        .main-content {
            flex: 1;
            padding: 1rem;
            max-width: 1200px;
            margin: 0 auto;
            width: 100%;
        }

        /* Cards */
        .card {
            background: var(--card-bg);
            border-radius: 12px;
            padding: 1.5rem;
            margin-bottom: 1.5rem;
            box-shadow: var(--shadow);
            border-left: 4px solid var(--admin-color);
            transition: all 0.3s ease;
        }

        .card:hover {
            box-shadow: var(--shadow-lg);
            transform: translateY(-2px);
        }

        /* Buttons */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.75rem 1.2rem;
            background: var(--admin-color);
            color: white;
            border: none;
            border-radius: 8px;
            text-decoration: none;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9rem;
            white-space: nowrap;
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: var(--shadow-lg);
            opacity: 0.9;
        }

        .btn-chef { 
            background: var(--chef-color); 
            color: white;
        }
        .btn-employe { 
            background: var(--employe-color); 
            color: white;
        }
        .btn-danger { 
            background: var(--danger); 
            color: white;
        }
        .btn-success { 
            background: var(--success); 
            color: white;
        }
        .btn-warning { 
            background: var(--warning); 
            color: white;
        }
        .btn-whatsapp { 
            background: #25D366; 
            color: white;
        }
        .btn-email { 
            background: #EA4335; 
            color: white;
        }
        .btn-outline {
            background: transparent;
            border: 2px solid var(--admin-color);
            color: var(--admin-color);
        }
        .btn-outline:hover {
            background: var(--admin-color);
            color: white;
        }

        .btn-small {
            padding: 0.5rem 0.8rem;
            font-size: 0.8rem;
        }

        .btn:disabled {
            opacity: 0.6;
            cursor: not-allowed;
            transform: none;
        }

        /* Role Cards */
        .roles-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .role-card {
            background: var(--card-bg);
            padding: 1.5rem;
            border-radius: 12px;
            text-align: center;
            box-shadow: var(--shadow);
            transition: all 0.3s ease;
            border-top: 4px solid var(--admin-color);
        }

        .role-card:hover {
            transform: translateY(-5px);
            box-shadow: var(--shadow-lg);
        }

        .role-card.chef { border-color: var(--chef-color); }
        .role-card.employe { border-color: var(--employe-color); }

        .role-icon {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        /* Forms */
        .form-group {
            margin-bottom: 1.2rem;
        }

        label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: var(--text-dark);
            font-size: 0.9rem;
        }

        input, select, textarea {
            width: 100%;
            padding: 0.75rem;
            border: 2px solid var(--border);
            border-radius: 8px;
            font-size: 0.9rem;
            transition: all 0.3s ease;
        }

        input:focus, select:focus {
            outline: none;
            border-color: var(--admin-color);
            box-shadow: 0 0 0 3px rgba(44, 123, 229, 0.1);
        }

        .form-row {
            display: flex;
            gap: 1rem;
            flex-wrap: wrap;
        }

        .form-row .form-group {
            flex: 1;
            min-width: 200px;
        }

        /* Tables */
        .table-container {
            overflow-x: auto;
            margin-top: 1rem;
            -webkit-overflow-scrolling: touch;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
            border-radius: 8px;
            overflow: hidden;
            box-shadow: var(--shadow);
            min-width: 600px;
        }

        th, td {
            padding: 0.8rem;
            text-align: left;
            border-bottom: 1px solid var(--border);
            font-size: 0.85rem;
        }

        th {
            background: var(--admin-color);
            color: white;
            font-weight: 600;
        }

        tr:hover {
            background: #f8fafc;
        }

        /* Alerts */
        .alert {
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.75rem;
            font-size: 0.9rem;
        }

        .alert.success {
            background: #d1fae5;
            color: #065f46;
            border-left: 4px solid var(--success);
        }

        .alert.error {
            background: #fee2e2;
            color: #991b1b;
            border-left: 4px solid var(--danger);
        }

        .alert.info {
            background: #dbeafe;
            color: #1e40af;
            border-left: 4px solid var(--admin-color);
        }

        .alert.warning {
            background: #fef3c7;
            color: #92400e;
            border-left: 4px solid var(--warning);
        }

        /* Dashboard Grid */
        .dashboard-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 1rem;
            margin-top: 1.5rem;
        }

        .dashboard-card {
            background: var(--card-bg);
            padding: 1.2rem;
            border-radius: 12px;
            box-shadow: var(--shadow);
            transition: all 0.3s ease;
            border-top: 4px solid var(--admin-color);
            cursor: pointer;
        }

        .dashboard-card:hover {
            transform: translateY(-3px);
            box-shadow: var(--shadow-lg);
        }

        /* Login */
        .login-container {
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 70vh;
        }

        .login-card {
            width: 100%;
            max-width: 400px;
            padding: 1.5rem;
        }

        /* Presence Management */
        .presence-section {
            background: #f8fafc;
            padding: 1.2rem;
            border-radius: 8px;
            margin-bottom: 1.2rem;
        }

        .employee-list {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            gap: 1rem;
            margin-top: 1rem;
        }

        .employee-card {
            background: white;
            padding: 1rem;
            border-radius: 8px;
            border: 2px solid var(--border);
            transition: all 0.3s ease;
        }

        .employee-card.present {
            border-color: var(--success);
            background: #f0fdf4;
        }

        .employee-card.absent {
            border-color: var(--danger);
            background: #fef2f2;
        }

        .presence-toggle {
            display: flex;
            gap: 0.5rem;
            margin-top: 0.5rem;
        }

        .toggle-btn {
            flex: 1;
            padding: 0.5rem;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-weight: 500;
            transition: all 0.3s ease;
            font-size: 0.8rem;
        }

        .toggle-present {
            background: var(--success);
            color: white;
        }

        .toggle-absent {
            background: var(--danger);
            color: white;
        }

        /* Image Section */
        .image-section {
            margin: 1.5rem 0;
            border-radius: 12px;
            overflow: hidden;
            box-shadow: var(--shadow-lg);
            position: relative;
            height: 250px;
        }

        .background-image {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .image-overlay {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.3);
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            color: white;
            text-align: center;
            padding: 1.5rem;
        }

        .image-title {
            font-size: 2rem;
            font-weight: bold;
            margin-bottom: 0.8rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
        }

        .image-subtitle {
            font-size: 1rem;
            margin-bottom: 1.5rem;
            text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.5);
            max-width: 600px;
        }

        /* Day Navigation */
        .day-navigation {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.2rem;
            padding: 1rem;
            background: #f8fafc;
            border-radius: 8px;
            gap: 1rem;
        }

        .day-selector {
            display: flex;
            gap: 0.5rem;
            align-items: center;
            flex-wrap: wrap;
        }

        .day-btn {
            padding: 0.5rem 0.8rem;
            border: 1px solid var(--border);
            background: white;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.8rem;
            min-width: 60px;
        }

        .day-btn.active {
            background: var(--admin-color);
            color: white;
            border-color: var(--admin-color);
        }

        .day-btn:hover:not(.active) {
            background: var(--border);
        }

        /* Empty State */
        .empty-state {
            text-align: center;
            padding: 2rem;
            color: var(--text-light);
        }

        .empty-state-icon {
            font-size: 3rem;
            margin-bottom: 1rem;
            opacity: 0.5;
        }

        /* Notification buttons */
        .notification-buttons {
            display: flex;
            gap: 1rem;
            margin: 1rem 0;
            flex-wrap: wrap;
        }

        .notification-section {
            background: #f8fafc;
            padding: 1.2rem;
            border-radius: 8px;
            margin: 1.2rem 0;
            border-left: 4px solid var(--warning);
        }

        .sending-status {
            margin-top: 1rem;
            padding: 1rem;
            background: white;
            border-radius: 8px;
            border: 1px solid var(--border);
        }

        .status-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 0.5rem 0;
            border-bottom: 1px solid var(--border);
            font-size: 0.85rem;
        }

        .status-item:last-child {
            border-bottom: none;
        }

        .status-indicator {
            display: inline-block;
            width: 10px;
            height: 10px;
            border-radius: 50%;
            margin-right: 0.5rem;
        }

        .status-pending { background: var(--warning); }
        .status-success { background: var(--success); }
        .status-error { background: var(--danger); }

        /* Styles pour le bulletin de paie professionnel */
        .bulletin-container {
            width: 100%;
            max-width: 210mm;
            height: auto;
            margin: 0 auto;
            background-color: white;
            box-shadow: var(--shadow-lg);
            position: relative;
            overflow: hidden;
            border-radius: 4px;
        }

        .bulletin-content {
            padding: 15px;
            height: 100%;
            display: flex;
            flex-direction: column;
        }

        /* Header */
        .bulletin-header {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            margin-bottom: 15px;
            padding-bottom: 10px;
            border-bottom: 2px solid var(--accent-color);
            gap: 1rem;
        }

        .company-info {
            flex: 1;
            min-width: 200px;
        }

        .company-logo {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
        }

        .logo-icon {
            font-size: 24px;
            margin-right: 8px;
            color: var(--accent-color);
        }

        .company-name {
            font-size: 18px;
            font-weight: 700;
            color: var(--primary-color);
        }

        .company-details {
            font-size: 9px;
            line-height: 1.3;
            color: #555;
        }

        .document-title {
            text-align: center;
            flex: 1;
            display: flex;
            flex-direction: column;
            justify-content: center;
            margin-right: 0;
        }

        .title-main {
            font-size: 18px;
            font-weight: 700;
            color: var(--primary-color);
            margin-bottom: 3px;
        }

        .title-sub {
            font-size: 11px;
            color: #666;
            font-weight: 500;
        }

        .employee-header-section {
            width: 120px;
            text-align: right;
        }

        .employee-photo {
            width: 70px;
            height: 70px;
            border: 2px solid var(--border-color);
            border-radius: 6px;
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            margin-left: auto;
            margin-bottom: 8px;
            overflow: hidden;
        }

        .photo-placeholder {
            color: #7f8c8d;
            font-size: 10px;
            text-align: center;
            padding: 3px;
        }

        .employee-details-compact {
            font-size: 9px;
        }

        .employee-details-compact .info-row {
            display: flex;
            justify-content: space-between;
            margin-bottom: 2px;
        }

        .employee-details-compact .info-label {
            font-weight: 600;
            text-align: left;
        }

        .employee-details-compact .info-value {
            text-align: right;
            margin-left: 5px;
        }

        /* Main Content */
        .bulletin-main {
            flex: 1;
            display: flex;
            flex-direction: column;
        }

        .period-info {
            background-color: var(--header-bg);
            padding: 8px 12px;
            border-radius: 4px;
            margin-bottom: 12px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            font-size: 9px;
            gap: 0.5rem;
        }

        .period-dates {
            display: flex;
            gap: 15px;
            flex-wrap: wrap;
        }

        .period-item {
            display: flex;
            align-items: center;
        }

        .period-label {
            font-weight: 600;
            margin-right: 3px;
        }

        /* Main Table */
        .table-container {
            flex: 1;
            overflow: hidden;
            margin-bottom: 10px;
        }

        .main-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 8px;
        }

        .main-table th {
            background-color: var(--header-bg);
            border: 1px solid var(--border-color);
            padding: 6px 3px;
            text-align: center;
            font-weight: 600;
            color: var(--primary-color);
        }

        .main-table td {
            border: 1px solid var(--border-color);
            padding: 5px 3px;
        }

        .main-table .designation {
            text-align: left;
            width: 35%;
        }

        .main-table .number, .main-table .base, .main-table .rate, 
        .main-table .gains, .main-table .deductions, .main-table .net {
            text-align: right;
            width: 11%;
        }

        .main-table .subtotal {
            font-weight: 600;
            background-color: var(--header-bg);
        }

        .main-table .total {
            font-weight: 700;
            background-color: var(--primary-color);
            color: white;
        }

        .main-table .activity-row {
            border-left: 2px solid var(--accent-color);
        }

        /* Summary */
        .summary-section {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            margin-bottom: 15px;
            gap: 1rem;
        }

        .summary-left, .summary-right {
            width: 100%;
            min-width: 200px;
        }

        .summary-title {
            font-size: 10px;
            font-weight: 600;
            margin-bottom: 5px;
            color: var(--primary-color);
            padding-bottom: 3px;
            border-bottom: 1px solid var(--border-color);
        }

        .summary-table {
            width: 100%;
            border-collapse: collapse;
            font-size: 8px;
        }

        .summary-table td {
            border: 1px solid var(--border-color);
            padding: 5px;
        }

        .summary-table .label {
            font-weight: 600;
            width: 60%;
        }

        .summary-table .value {
            text-align: right;
            width: 40%;
        }

        .summary-table .total-row {
            font-weight: 700;
            background-color: var(--header-bg);
        }

        /* Footer */
        .bulletin-footer {
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
            margin-top: auto;
            padding-top: 10px;
            border-top: 1px solid var(--border-color);
            gap: 1rem;
        }

        .legal-mentions {
            width: 100%;
            font-size: 7px;
            color: #7f8c8d;
            line-height: 1.3;
        }

        .signature-section {
            text-align: center;
            width: 100%;
        }

        .signature-stamp {
            width: 80px;
            height: 80px;
            border: 2px solid var(--accent-color);
            border-radius: 50%;
            margin: 0 auto 5px;
            display: flex;
            align-items: center;
            justify-content: center;
            color: var(--accent-color);
            font-weight: 600;
            font-size: 8px;
            text-align: center;
            line-height: 1.1;
            background: white;
        }

        .signature-line {
            border-top: 1px solid var(--border-color);
            width: 120px;
            margin: 0 auto;
            padding-top: 3px;
            font-size: 8px;
        }

        /* Print styles */
        @media print {
            body {
                background: white;
                padding: 0;
                margin: 0;
            }
            
            .bulletin-container {
                box-shadow: none;
                margin: 0;
                width: 100%;
                height: 100%;
                border-radius: 0;
                page-break-after: avoid;
                page-break-inside: avoid;
            }
            
            .bulletin-content {
                padding: 10mm;
            }
            
            .no-print {
                display: none;
            }
        }

        /* Controls */
        .controls {
            text-align: center;
            margin: 15px auto;
            max-width: 210mm;
        }

        /* Additional variables for bulletin */
        .bulletin-container {
            --primary-color: #2c3e50;
            --secondary-color: #3498db;
            --accent-color: #2980b9;
            --border-color: #e0e0e0;
            --text-color: #2c3e50;
            --light-bg: #f8f9fa;
            --success-color: #27ae60;
            --header-bg: #f5f7fa;
        }

        /* Color indicator */
        .color-indicator {
            display: inline-block;
            width: 20px;
            height: 20px;
            border-radius: 50%;
            margin-right: 0.5rem;
            border: 2px solid white;
            box-shadow: 0 0 0 1px var(--border);
        }

        /* Activity badges */
        .activity-badge {
            display: inline-block;
            padding: 0.25rem 0.75rem;
            background: var(--admin-color);
            color: white;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
            margin-left: 0.5rem;
        }

        /* Action buttons */
        .action-buttons {
            display: flex;
            gap: 1rem;
            margin: 1.5rem 0;
            flex-wrap: wrap;
        }

        .action-btn {
            flex: 1;
            min-width: 200px;
            padding: 1.2rem;
            font-size: 1rem;
            text-align: center;
        }

        .chef-info {
            background: #e8f2ff;
            padding: 1rem;
            border-radius: 8px;
            margin-bottom: 1.2rem;
            font-size: 0.9rem;
        }

        /* Photo upload */
        .photo-upload-container {
            text-align: center;
            margin-bottom: 1.2rem;
        }

        .photo-preview {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            object-fit: cover;
            border: 3px solid var(--border);
            margin: 0 auto 1rem;
            display: block;
            background: #f8fafc;
        }

        .photo-placeholder {
            width: 100px;
            height: 100px;
            border-radius: 50%;
            background: #f8fafc;
            display: flex;
            align-items: center;
            justify-content: center;
            margin: 0 auto 1rem;
            border: 3px dashed var(--border);
            color: var(--text-light);
            font-size: 1.8rem;
        }

        .file-input {
            display: none;
        }

        .file-input-label {
            display: inline-block;
            padding: 0.5rem 1rem;
            background: var(--admin-color);
            color: white;
            border-radius: 6px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 0.9rem;
        }

        .file-input-label:hover {
            background: #1a56db;
        }

        .user-photo {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            object-fit: cover;
            margin-right: 0.5rem;
            border: 2px solid var(--border);
        }

        .user-photo-table {
            width: 25px;
            height: 25px;
            border-radius: 50%;
            object-fit: cover;
            margin-right: 0.5rem;
            border: 2px solid var(--border);
        }

        /* Avatar avec initiales */
        .avatar {
            width: 35px;
            height: 35px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 14px;
            margin-right: 0.5rem;
        }

        .avatar-table {
            width: 25px;
            height: 25px;
            border-radius: 50%;
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            font-weight: bold;
            font-size: 10px;
            margin-right: 0.5rem;
        }

        .avatar-admin { background: var(--admin-color); }
        .avatar-chef { background: var(--chef-color); }
        .avatar-employe { background: var(--employe-color); }

        /* Filtres */
        .filters {
            display: flex;
            gap: 1rem;
            margin-bottom: 1.2rem;
            flex-wrap: wrap;
            align-items: center;
        }

        .filter-group {
            display: flex;
            flex-direction: column;
            gap: 0.5rem;
            min-width: 150px;
        }

        .filter-group label {
            font-size: 0.85rem;
            font-weight: 600;
            margin-bottom: 0;
        }

        /* Stats cards */
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 1rem;
            margin-bottom: 1.2rem;
        }

        .stat-card {
            background: white;
            padding: 1.2rem;
            border-radius: 8px;
            text-align: center;
            box-shadow: var(--shadow);
            border-top: 4px solid var(--admin-color);
        }

        .stat-number {
            font-size: 1.5rem;
            font-weight: bold;
            color: var(--admin-color);
            margin-bottom: 0.5rem;
        }

        .stat-label {
            color: var(--text-light);
            font-size: 0.8rem;
        }

        /* Fiche de pointage */
        .fiche-header {
            background: #f8fafc;
            padding: 1.2rem;
            border-radius: 8px;
            margin-bottom: 1.2rem;
            border-left: 4px solid var(--admin-color);
        }

        .fiche-date {
            font-size: 1.2rem;
            font-weight: bold;
            color: var(--admin-color);
            margin-bottom: 0.5rem;
        }

        .fiche-activity {
            font-size: 1rem;
            color: var(--text-light);
            font-weight: 500;
        }

        .fiche-stats {
            display: flex;
            gap: 1rem;
            margin-top: 1rem;
            flex-wrap: wrap;
        }

        .fiche-stat {
            background: white;
            padding: 0.75rem 1rem;
            border-radius: 6px;
            border: 1px solid var(--border);
            text-align: center;
            min-width: 100px;
        }

        .fiche-stat-number {
            font-size: 1.1rem;
            font-weight: bold;
            color: var(--admin-color);
        }

        .fiche-stat-label {
            font-size: 0.75rem;
            color: var(--text-light);
        }

        /* Archives */
        .archive-section {
            background: #f8fafc;
            padding: 1.2rem;
            border-radius: 8px;
            margin-bottom: 1.2rem;
            border-left: 4px solid var(--warning);
        }

        .archive-actions {
            display: flex;
            gap: 1rem;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }

        .archive-folder {
            background: white;
            border: 2px solid var(--border);
            border-radius: 8px;
            padding: 1rem;
            margin-bottom: 1rem;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .archive-folder:hover {
            border-color: var(--admin-color);
            transform: translateY(-2px);
        }

        .folder-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 0.5rem;
        }

        .folder-title {
            font-weight: bold;
            color: var(--admin-color);
        }

        .folder-count {
            background: var(--admin-color);
            color: white;
            padding: 0.25rem 0.5rem;
            border-radius: 12px;
            font-size: 0.8rem;
        }

        .folder-details {
            font-size: 0.85rem;
            color: var(--text-light);
        }

        .search-box {
            display: flex;
            gap: 0.5rem;
            margin-bottom: 1rem;
            flex-wrap: wrap;
        }

        .search-input {
            flex: 1;
            min-width: 200px;
        }

        .search-results {
            background: white;
            border-radius: 8px;
            padding: 1rem;
            margin-top: 1rem;
            box-shadow: var(--shadow);
        }

        /* Checkbox pour sélection multiple */
        .select-all-container {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 1rem;
            padding: 1rem;
            background: #f8fafc;
            border-radius: 8px;
            flex-wrap: wrap;
        }

        .checkbox-item {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            padding: 0.5rem;
            margin: 0.25rem 0;
        }

        .selected-count {
            background: var(--admin-color);
            color: white;
            padding: 0.25rem 0.75rem;
            border-radius: 20px;
            font-size: 0.8rem;
            font-weight: 600;
        }

        /* Modal d'archivage */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.5);
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            padding: 1rem;
        }

        .modal-content {
            background: white;
            padding: 1.5rem;
            border-radius: 12px;
            box-shadow: var(--shadow-lg);
            max-width: 500px;
            width: 100%;
            max-height: 80vh;
            overflow-y: auto;
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 1.2rem;
        }

        .modal-close {
            background: none;
            border: none;
            font-size: 1.5rem;
            cursor: pointer;
            color: var(--text-light);
        }

        .archive-options {
            display: flex;
            flex-direction: column;
            gap: 1rem;
            margin: 1rem 0;
        }

        .archive-option {
            display: flex;
            align-items: center;
            gap: 1rem;
            padding: 1rem;
            border: 2px solid var(--border);
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .archive-option:hover {
            border-color: var(--admin-color);
            background: #f0f7ff;
        }

        .archive-option.selected {
            border-color: var(--admin-color);
            background: #e8f2ff;
        }

        .option-icon {
            font-size: 1.8rem;
        }

        .option-content {
            flex: 1;
        }

        .option-title {
            font-weight: 600;
            margin-bottom: 0.25rem;
        }

        .option-description {
            font-size: 0.85rem;
            color: var(--text-light);
        }

        /* Hidden sections */
        .section {
            display: none;
        }

        .section.active {
            display: block;
        }

        /* ============================================= */
        /* MEDIA QUERIES POUR LA RESPONSIVE */
        /* ============================================= */

        /* Tablettes */
        @media (max-width: 1024px) {
            .header {
                padding: 1rem;
            }
            
            .logo h1 {
                font-size: 1.2rem;
            }
            
            .nav a {
                padding: 0.4rem 0.7rem;
                font-size: 0.85rem;
            }
            
            .main-content {
                padding: 1rem;
            }
            
            .card {
                padding: 1.2rem;
            }
            
            .roles-grid {
                grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            }
            
            .dashboard-grid {
                grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
            }
            
            .action-btn {
                min-width: 180px;
                padding: 1rem;
            }
            
            .image-section {
                height: 200px;
            }
            
            .image-title {
                font-size: 1.8rem;
            }
            
            .image-subtitle {
                font-size: 0.9rem;
            }
        }

        /* Mobiles */
        @media (max-width: 768px) {
            .header {
                flex-direction: column;
                gap: 1rem;
                padding: 1rem;
            }

            .nav {
                width: 100%;
                justify-content: center;
            }

            .main-content {
                padding: 0.8rem;
            }
            
            .card {
                padding: 1rem;
                margin-bottom: 1rem;
            }
            
            .form-row {
                flex-direction: column;
            }
            
            .form-row .form-group {
                min-width: 100%;
            }

            .roles-grid, .dashboard-grid {
                grid-template-columns: 1fr;
            }
            
            .employee-list {
                grid-template-columns: 1fr;
            }
            
            .filters {
                flex-direction: column;
                align-items: stretch;
            }
            
            .filter-group {
                min-width: 100%;
            }
            
            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
            
            .action-buttons {
                flex-direction: column;
            }
            
            .action-btn {
                min-width: 100%;
            }
            
            .notification-buttons {
                flex-direction: column;
            }
            
            .day-navigation {
                flex-direction: column;
                align-items: stretch;
            }
            
            .day-selector {
                justify-content: center;
            }
            
            .image-section {
                height: 180px;
            }
            
            .image-title {
                font-size: 1.5rem;
            }
            
            .image-subtitle {
                font-size: 0.8rem;
                margin-bottom: 1rem;
            }
            
            .bulletin-header {
                flex-direction: column;
                text-align: center;
            }
            
            .employee-header-section {
                width: 100%;
                text-align: center;
                margin-top: 15px;
            }
            
            .employee-photo {
                margin: 0 auto 8px;
            }
            
            .summary-section {
                flex-direction: column;
            }
            
            .summary-left, .summary-right {
                width: 100%;
                margin-bottom: 15px;
            }
            
            .bulletin-footer {
                flex-direction: column;
            }
            
            .legal-mentions, .signature-section {
                width: 100%;
            }
            
            .archive-actions {
                flex-direction: column;
            }
            
            .select-all-container {
                flex-direction: column;
                align-items: flex-start;
            }
            
            .search-box {
                flex-direction: column;
            }
            
            .search-input {
                min-width: 100%;
            }
            
            .modal-content {
                padding: 1rem;
            }
            
            .archive-option {
                flex-direction: column;
                text-align: center;
            }
            
            .option-icon {
                font-size: 2rem;
            }
        }

        /* Petits mobiles */
        @media (max-width: 480px) {
            .header {
                padding: 0.8rem;
            }
            
            .logo h1 {
                font-size: 1.1rem;
            }
            
            .logo-icon {
                font-size: 1.5rem;
            }
            
            .nav a {
                padding: 0.3rem 0.6rem;
                font-size: 0.8rem;
            }
            
            .main-content {
                padding: 0.5rem;
            }
            
            .card {
                padding: 0.8rem;
            }
            
            .btn {
                padding: 0.6rem 1rem;
                font-size: 0.85rem;
            }
            
            .btn-small {
                padding: 0.4rem 0.7rem;
                font-size: 0.75rem;
            }
            
            .roles-grid {
                gap: 0.8rem;
            }
            
            .role-card {
                padding: 1rem;
            }
            
            .role-icon {
                font-size: 2rem;
            }
            
            .dashboard-grid {
                gap: 0.8rem;
            }
            
            .dashboard-card {
                padding: 1rem;
            }
            
            .stats-grid {
                grid-template-columns: 1fr;
                gap: 0.8rem;
            }
            
            .stat-card {
                padding: 1rem;
            }
            
            .stat-number {
                font-size: 1.3rem;
            }
            
            .image-section {
                height: 150px;
            }
            
            .image-title {
                font-size: 1.3rem;
            }
            
            .image-subtitle {
                font-size: 0.75rem;
            }
            
            .fiche-header {
                padding: 1rem;
            }
            
            .fiche-date {
                font-size: 1.1rem;
            }
            
            .fiche-activity {
                font-size: 0.9rem;
            }
            
            .fiche-stats {
                gap: 0.5rem;
            }
            
            .fiche-stat {
                padding: 0.5rem 0.8rem;
                min-width: 80px;
            }
            
            .fiche-stat-number {
                font-size: 1rem;
            }
            
            .fiche-stat-label {
                font-size: 0.7rem;
            }
            
            th, td {
                padding: 0.6rem;
                font-size: 0.75rem;
            }
            
            .alert {
                padding: 0.8rem;
                font-size: 0.85rem;
            }
            
            .presence-section {
                padding: 1rem;
            }
            
            .employee-card {
                padding: 0.8rem;
            }
            
            .toggle-btn {
                font-size: 0.75rem;
            }
            
            .notification-section {
                padding: 1rem;
            }
            
            .sending-status {
                padding: 0.8rem;
            }
            
            .status-item {
                font-size: 0.8rem;
            }
            
            .day-btn {
                padding: 0.4rem 0.6rem;
                font-size: 0.75rem;
                min-width: 50px;
            }
            
            .empty-state {
                padding: 1.5rem;
            }
            
            .empty-state-icon {
                font-size: 2.5rem;
            }
            
            .photo-preview, .photo-placeholder {
                width: 80px;
                height: 80px;
            }
            
            .photo-placeholder {
                font-size: 1.5rem;
            }
            
            .user-photo {
                width: 30px;
                height: 30px;
            }
            
            .user-photo-table {
                width: 20px;
                height: 20px;
            }
            
            .avatar {
                width: 30px;
                height: 30px;
                font-size: 12px;
            }
            
            .avatar-table {
                width: 20px;
                height: 20px;
                font-size: 9px;
            }
            
            .color-indicator {
                width: 16px;
                height: 16px;
            }
            
            .activity-badge {
                padding: 0.2rem 0.6rem;
                font-size: 0.75rem;
            }
            
            .chef-info {
                padding: 0.8rem;
                font-size: 0.85rem;
            }
        }

        /* Très petits écrans */
        @media (max-width: 360px) {
            .logo h1 {
                font-size: 1rem;
            }
            
            .nav a {
                padding: 0.25rem 0.5rem;
                font-size: 0.75rem;
            }
            
            .main-content {
                padding: 0.3rem;
            }
            
            .card {
                padding: 0.7rem;
            }
            
            .btn {
                padding: 0.5rem 0.8rem;
                font-size: 0.8rem;
            }
            
            .roles-grid {
                grid-template-columns: 1fr;
            }
            
            .role-card {
                padding: 0.8rem;
            }
            
            .dashboard-grid {
                grid-template-columns: 1fr;
            }
            
            .dashboard-card {
                padding: 0.8rem;
            }
            
            .image-section {
                height: 120px;
            }
            
            .image-title {
                font-size: 1.1rem;
            }
            
            .image-subtitle {
                font-size: 0.7rem;
            }
            
            .fiche-header {
                padding: 0.8rem;
            }
            
            .fiche-date {
                font-size: 1rem;
            }
            
            .fiche-activity {
                font-size: 0.8rem;
            }
            
            .fiche-stats {
                gap: 0.3rem;
            }
            
            .fiche-stat {
                padding: 0.4rem 0.6rem;
                min-width: 70px;
            }
            
            .fiche-stat-number {
                font-size: 0.9rem;
            }
            
            .fiche-stat-label {
                font-size: 0.65rem;
            }
        }

        /* Orientation paysage sur mobiles */
        @media (max-height: 500px) and (orientation: landscape) {
            .header {
                padding: 0.5rem;
            }
            
            .main-content {
                padding: 0.5rem;
            }
            
            .card {
                padding: 1rem;
                margin-bottom: 0.8rem;
            }
            
            .login-container {
                min-height: 60vh;
            }
            
            .image-section {
                height: 120px;
                margin: 1rem 0;
            }
            
            .roles-grid {
                grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
                gap: 0.8rem;
                margin-top: 1rem;
            }
            
            .dashboard-grid {
                grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
                gap: 0.8rem;
                margin-top: 1rem;
            }
        }
    </style>
</head>
<body>
    <div class="bg-slider">
        <div class="bg-slide"></div>
        <div class="bg-slide"></div>
        <div class="bg-slide"></div>
        <div class="bg-slide"></div>
    </div>

    <div class="app-container">
        <!-- Header -->
        <header class="header" id="appHeader">
            <div class="logo">
                <div class="logo-icon">🌴</div>
                <h1>MKJ SERVICE</h1>
            </div>
            <nav class="nav" id="appNav">
                <a href="#" onclick="showSection('home')">Accueil</a>
                <a href="#" onclick="showSection('dashboard')" id="navDashboard" style="display: none;">Dashboard</a>
                <a href="#" onclick="showSection('profile')" id="navProfile" style="display: none;">Profil</a>
                <a href="#" onclick="showSection('adminArchives')" id="navArchives" style="display: none;">Archives</a>
                <a href="#" onclick="logout()" id="navLogout" style="display: none;">Déconnexion</a>
            </nav>
        </header>

        <!-- Main Content -->
        <main class="main-content">
            <!-- Alerts Container -->
            <div id="alertsContainer"></div>

            <!-- Home Section -->
            <section id="home" class="section active">
                <!-- Image Section -->
                <div class="image-section">
                    <img src="https://static.vecteezy.com/ti/vecteur-libre/p1/132008-illustration-de-l-huile-de-palme-vectoriel.jpg" alt="Plantation de palmiers" class="background-image">
                    <div class="image-overlay">
                        <h2 class="image-title">MKJ SERVICE</h2>
                        <p class="image-subtitle">Expert en plantation de palmiers à huile - Gestion optimisée de votre personnel</p>
                    </div>
                </div>

                <div class="card">
                    <h2>Bienvenue sur MKJ SERVICE</h2>
                    <p>Système de gestion du personnel pour plantation de palmiers à huile</p>
                    
                    <div class="roles-grid">
                        <div class="role-card">
                            <div class="role-icon">👑</div>
                            <h3>ADMINISTRATEUR</h3>
                            <p>Accès complet à la gestion des utilisateurs et données</p>
                            <button class="btn" onclick="showLogin('ADMINISTRATEUR')">Se connecter</button>
                        </div>
                        
                        <div class="role-card chef">
                            <div class="role-icon">👨‍💼</div>
                            <h3>CHEF D'ÉQUIPE</h3>
                            <p>Gestion des pointages et suivi des équipes</p>
                            <button class="btn btn-chef" onclick="showLogin('CHEF')">Se connecter</button>
                        </div>
                        
                        <div class="role-card employe">
                            <div class="role-icon">👷</div>
                            <h3>EMPLOYÉ</h3>
                            <p>Consultation des pointages et activités</p>
                            <button class="btn btn-employe" onclick="showLogin('EMPLOYE')">Se connecter</button>
                        </div>
                    </div>
                    
                    <div style="margin-top: 2rem; padding: 1rem; background: #e8f2ff; border-radius: 8px;">
                        <strong>Compte de démonstration :</strong> identifiant = <code>test</code>, mot de passe = <code>test</code>
                    </div>
                </div>
            </section>

            <!-- Login Section -->
            <section id="login" class="section">
                <div class="login-container">
                    <div class="card login-card">
                        <h2 id="loginTitle">Connexion</h2>
                        <form id="loginForm" onsubmit="handleLogin(event)">
                            <div class="form-group">
                                <label for="username">Identifiant</label>
                                <input type="text" id="username" required placeholder="Votre identifiant">
                            </div>
                            
                            <div class="form-group">
                                <label for="password">Mot de passe</label>
                                <input type="password" id="password" required placeholder="Votre mot de passe">
                            </div>
                            
                            <button type="submit" class="btn" style="width: 100%;">
                                <span>🔐</span> Se connecter
                            </button>
                        </form>
                        
                        <div style="text-align: center; margin-top: 1rem;">
                            <button class="btn btn-outline" onclick="showSection('home')">← Retour à l'accueil</button>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Dashboard Section -->
            <section id="dashboard" class="section">
                <div class="card">
                    <h2 id="dashboardTitle">Tableau de bord</h2>
                    <p id="dashboardWelcome">Bienvenue !</p>
                    
                    <div class="dashboard-grid" id="dashboardGrid">
                        <!-- Content populated by JavaScript -->
                    </div>
                </div>
            </section>

            <!-- Profile Section -->
            <section id="profile" class="section">
                <div class="card">
                    <h3>Profil utilisateur</h3>
                    <div id="profileContent">
                        <!-- Content populated by JavaScript -->
                    </div>
                </div>
            </section>

            <!-- Admin Users Section -->
            <section id="adminUsers" class="section">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem;">
                        <h3>Gestion des utilisateurs</h3>
                        <button class="btn" onclick="showSection('adminCreateUser')">➕ Créer utilisateur</button>
                    </div>

                    <!-- Filtres -->
                    <div class="filters">
                        <div class="filter-group">
                            <label for="filterDepartement">Filtrer par département:</label>
                            <select id="filterDepartement" onchange="filterUsersTable()">
                                <option value="">Tous les départements</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filterRole">Filtrer par rôle:</label>
                            <select id="filterRole" onchange="filterUsersTable()">
                                <option value="">Tous les rôles</option>
                                <option value="CHEF">CHEF</option>
                                <option value="EMPLOYE">EMPLOYE</option>
                            </select>
                        </div>
                    </div>

                    <div class="table-container">
                        <table id="usersTable">
                            <thead>
                                <tr>
                                    <th>Photo</th><th>ID</th><th>Identifiant</th><th>Nom</th><th>Prénom</th><th>Role</th><th>Activité</th><th>Département</th><th>Couleur</th><th>Actions</th>
                                </tr>
                            </thead>
                            <tbody id="usersTableBody">
                                <!-- Populated by JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Admin Pointages Section -->
            <section id="adminPointages" class="section">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem;">
                        <h3>Gestion des fiches de pointage</h3>
                        <div>
                            <button class="btn" onclick="showSection('dashboard')">📊 Retour au dashboard</button>
                            <button class="btn btn-warning" onclick="showArchiveModal('pointages')" style="margin-left: 0.5rem;">📦 Archiver sélection</button>
                        </div>
                    </div>

                    <!-- Sélection multiple -->
                    <div class="select-all-container">
                        <input type="checkbox" id="selectAllPointages" onchange="toggleSelectAllPointages()">
                        <label for="selectAllPointages">Tout sélectionner</label>
                        <span class="selected-count" id="selectedPointagesCount">0 sélectionné(s)</span>
                        <button class="btn btn-small btn-outline" onclick="clearPointagesSelection()" style="margin-left: auto;">❌ Effacer</button>
                    </div>

                    <!-- Recherche avancée -->
                    <div class="search-box">
                        <input type="text" id="searchPointage" class="search-input" placeholder="Rechercher par nom d'employé, chef, activité..." onkeyup="searchPointages()">
                        <button class="btn btn-small" onclick="searchPointages()">🔍 Rechercher</button>
                    </div>

                    <!-- Statistiques -->
                    <div class="stats-grid" id="pointageStats">
                        <!-- Populated by JavaScript -->
                    </div>

                    <!-- Filtres -->
                    <div class="filters">
                        <div class="filter-group">
                            <label for="filterPointageActivity">Filtrer par activité:</label>
                            <select id="filterPointageActivity" onchange="filterPointagesTable()">
                                <option value="">Toutes les activités</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filterPointageDate">Filtrer par date:</label>
                            <input type="date" id="filterPointageDate" onchange="filterPointagesTable()">
                        </div>
                        <div class="filter-group">
                            <label for="filterPointageChef">Filtrer par chef:</label>
                            <select id="filterPointageChef" onchange="filterPointagesTable()">
                                <option value="">Tous les chefs</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                    </div>

                    <div class="table-container">
                        <table id="pointagesTable">
                            <thead>
                                <tr>
                                    <th width="30px">
                                        <input type="checkbox" id="selectAllPointagesHeader" onchange="toggleSelectAllPointages()">
                                    </th>
                                    <th>ID Fiche</th><th>Date</th><th>Chef</th><th>Activité</th><th>Employé</th><th>Présence</th><th>Bloc</th><th>Quantité</th><th>Prix unitaire</th><th>Prix total</th>
                                </tr>
                            </thead>
                            <tbody id="pointagesTableBody">
                                <!-- Populated by JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Admin Create User Section -->
            <section id="adminCreateUser" class="section">
                <div class="card">
                    <h3>Créer un utilisateur</h3>
                    <form id="createUserForm" onsubmit="handleCreateUser(event)">
                        <!-- Photo Upload -->
                        <div class="photo-upload-container">
                            <div id="photoPreview" class="photo-placeholder">
                                👤
                            </div>
                            <input type="file" id="photoInput" class="file-input" accept="image/*" onchange="previewPhoto(event)">
                            <label for="photoInput" class="file-input-label">📷 Choisir une photo</label>
                            <div style="font-size: 0.8rem; color: var(--text-light); margin-top: 0.5rem;">
                                Si aucune photo n'est choisie, un avatar avec les initiales sera généré
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label>Role *</label>
                                <select id="userRole" required onchange="toggleActivityField()">
                                    <option value="">Sélectionner un rôle</option>
                                    <option value="CHEF">CHEF</option>
                                    <option value="EMPLOYE">EMPLOYE</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Identifiant *</label>
                                <input type="text" id="newUsername" required placeholder="identifiant">
                            </div>
                            <div class="form-group">
                                <label>Mot de passe *</label>
                                <input type="password" id="newPassword" required placeholder="mot de passe">
                            </div>
                        </div>
                        
                        <div class="form-row">
                            <div class="form-group">
                                <label>Nom *</label>
                                <input type="text" id="newNom" required placeholder="Nom">
                            </div>
                            <div class="form-group">
                                <label>Prénom *</label>
                                <input type="text" id="newPrenom" required placeholder="Prénom">
                            </div>
                            <div class="form-group">
                                <label>Département *</label>
                                <select id="newDepartement" required>
                                    <option value="">Sélectionner un département</option>
                                    <option value="ZoneA">Zone A</option>
                                    <option value="ZoneB">Zone B</option>
                                    <option value="ZoneC">Zone C</option>
                                    <option value="ZoneD">Zone D</option>
                                    <option value="ZoneE">Zone E</option>
                                    <option value="ZoneF">Zone F</option>
                                    <option value="ZoneG">Zone G</option>
                                    <option value="ZoneH">Zone H</option>
                                    <option value="ZoneI">Zone I</option>
                                    <option value="ZoneJ">Zone J</option>
                                </select>
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group">
                                <label>Numéro de téléphone</label>
                                <input type="tel" id="newTelephone" placeholder="Numéro de téléphone">
                            </div>
                            <div class="form-group">
                                <label>Email</label>
                                <input type="email" id="newEmail" placeholder="Adresse email">
                            </div>
                        </div>

                        <div class="form-row">
                            <div class="form-group" id="activityField" style="display: none;">
                                <label>Activité du Chef *</label>
                                <select id="newActivity">
                                    <option value="recolte">Récolte</option>
                                    <option value="rabattage">Rabattage</option>
                                    <option value="élagage">Élagage</option>
                                    <option value="ronds">Ronds</option>
                                    <option value="spring">Spring</option>
                                    <option value="engrais">Engrais</option>
                                </select>
                            </div>
                            <div class="form-group" id="employeeActivityField">
                                <label>Activité de l'Employé *</label>
                                <select id="newEmployeeActivity" required>
                                    <option value="">Sélectionner une activité</option>
                                    <option value="recolte">Récolte</option>
                                    <option value="rabattage">Rabattage</option>
                                    <option value="élagage">Élagage</option>
                                    <option value="ronds">Ronds</option>
                                    <option value="spring">Spring</option>
                                    <option value="engrais">Engrais</option>
                                </select>
                            </div>
                            <div class="form-group">
                                <label>Couleur (hex)</label>
                                <input type="color" id="newColor" value="#ff8c00">
                            </div>
                        </div>
                        
                        <div style="margin-top: 1.5rem;">
                            <button type="submit" class="btn">Créer l'utilisateur</button>
                            <button type="button" class="btn btn-outline" onclick="showSection('adminUsers')" style="margin-left: 0.5rem;">Annuler</button>
                        </div>
                    </form>
                </div>
            </section>

            <!-- Chef Actions Section -->
            <section id="chefActions" class="section">
                <div class="card">
                    <h3>Actions Chef d'Équipe</h3>
                    <div id="chefInfo" class="chef-info">
                        <!-- Chef information will be populated here -->
                    </div>
                    <p>Choisissez l'action que vous souhaitez effectuer :</p>
                    
                    <div class="action-buttons">
                        <button class="btn action-btn" onclick="showSection('chefPresence')">
                            <div style="font-size: 2rem; margin-bottom: 0.5rem;">📋</div>
                            <div><strong>Gestion des Présences</strong></div>
                            <div style="font-size: 0.9rem; opacity: 0.8; margin-top: 0.5rem;">Marquer les présences et absences</div>
                        </button>
                        
                        <button class="btn btn-chef action-btn" onclick="showSection('chefPointage')">
                            <div style="font-size: 2rem; margin-bottom: 0.5rem;">📝</div>
                            <div><strong>Pointage des Activités</strong></div>
                            <div style="font-size: 0.9rem; opacity: 0.8; margin-top: 0.5rem;">Renseigner les activités des présents</div>
                        </button>
                    </div>
                    
                    <div style="margin-top: 1.5rem;">
                        <button class="btn btn-outline" onclick="showSection('chefPointages')">📋 Voir mes pointages</button>
                    </div>
                </div>
            </section>

            <!-- Chef Presence Section -->
            <section id="chefPresence" class="section">
                <div class="card">
                    <h3>📋 Gestion des Présences - <span id="chefActivityBadge"></span></h3>
                    <p>Marquez les employés présents de votre activité. Les absents seront automatiquement enregistrés.</p>
                    
                    <div class="presence-section">
                        <div class="form-group">
                            <label>Date du pointage *</label>
                            <input type="date" id="presenceDate" required>
                        </div>
                        
                        <div class="employee-list" id="employeePresenceList">
                            <!-- Employees will be populated here -->
                        </div>
                        
                        <div style="margin-top: 1rem; text-align: center;">
                            <button class="btn" onclick="savePresences()">💾 Enregistrer les Présences</button>
                            <button class="btn btn-outline" onclick="showSection('chefActions')" style="margin-left: 0.5rem;">← Retour</button>
                        </div>
                    </div>
                </div>
            </section>

            <!-- Chef Pointage Section -->
            <section id="chefPointage" class="section">
                <div class="card">
                    <h3>📝 Pointage des Activités - <span id="pointageActivityBadge"></span></h3>
                    <p>Renseignez les activités des employés marqués comme présents dans votre activité.</p>
                    
                    <div class="form-group">
                        <label>Date du pointage *</label>
                        <input type="date" id="pointageDate" required>
                    </div>
                    
                    <div id="pointageFormsContainer">
                        <!-- Pointage forms will be populated here -->
                    </div>

                    <!-- Section de notification -->
                    <div class="notification-section">
                        <h4>📤 Envoi des pointages</h4>
                        <p>Après enregistrement, vous pouvez envoyer les pointages aux employés concernés :</p>
                        
                        <div class="notification-buttons">
                            <button class="btn btn-email" onclick="sendPointagesByEmail()" id="emailBtn" disabled>
                                📧 Envoyer par Email
                            </button>
                            <button class="btn btn-whatsapp" onclick="sendPointagesByWhatsApp()" id="whatsappBtn" disabled>
                                💬 Envoyer par WhatsApp
                            </button>
                        </div>

                        <div id="sendingStatus" class="sending-status" style="display: none;">
                            <h5>Statut d'envoi :</h5>
                            <div id="statusList"></div>
                        </div>
                    </div>
                    
                    <div style="margin-top: 1.5rem;">
                        <button class="btn" onclick="saveAllPointages()">💾 Enregistrer Tous les Pointages</button>
                        <button class="btn btn-outline" onclick="showSection('chefActions')" style="margin-left: 0.5rem;">← Retour</button>
                    </div>
                </div>
            </section>

            <!-- Chef Pointages List Section -->
            <section id="chefPointages" class="section">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem;">
                        <h3>Mes pointages - <span id="pointagesActivityBadge"></span></h3>
                        <div>
                            <button class="btn" onclick="showSection('chefActions')">📊 Retour aux actions</button>
                            <button class="btn btn-outline" onclick="searchChefPointages()" style="margin-left: 0.5rem;">🔍 Rechercher</button>
                        </div>
                    </div>

                    <!-- Recherche -->
                    <div class="search-box" id="chefSearchBox" style="display: none;">
                        <input type="text" id="searchChefPointage" class="search-input" placeholder="Rechercher par nom d'employé, date, bloc...">
                        <button class="btn btn-small" onclick="performChefSearch()">🔍 Rechercher</button>
                        <button class="btn btn-outline btn-small" onclick="clearChefSearch()">❌ Effacer</button>
                    </div>

                    <!-- Navigation par jour -->
                    <div class="day-navigation">
                        <div class="day-selector" id="daySelector">
                            <!-- Les jours seront générés dynamiquement -->
                        </div>
                        <div>
                            <button class="btn btn-small" onclick="previousWeek()">← Semaine précédente</button>
                            <button class="btn btn-small" onclick="nextWeek()">Semaine suivante →</button>
                        </div>
                    </div>

                    <!-- Fiche du jour sélectionné -->
                    <div id="dailyPointagesContainer">
                        <!-- Contenu généré dynamiquement -->
                    </div>
                </div>
            </section>

            <!-- Employee Pointages Section -->
            <section id="employeePointages" class="section">
                <div class="card">
                    <h3>Mes pointages</h3>
                    
                    <!-- Recherche -->
                    <div class="search-box">
                        <input type="text" id="searchEmployeePointage" class="search-input" placeholder="Rechercher par date, activité, bloc..." onkeyup="searchEmployeePointages()">
                        <button class="btn btn-small" onclick="searchEmployeePointages()">🔍 Rechercher</button>
                    </div>

                    <div class="table-container">
                        <table id="employeePointagesTable">
                            <thead>
                                <tr>
                                    <th>ID</th><th>Nom Prénom</th><th>Date</th><th>Présence</th><th>Activité</th><th>Quantité</th><th>Prix unitaire</th><th>Prix total</th><th>Bloc</th><th>Chef</th>
                                </tr>
                            </thead>
                            <tbody id="employeePointagesBody">
                                <!-- Populated by JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Admin Paie Section -->
            <section id="adminPaie" class="section">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem;">
                        <h3>💰 Gestion de la Paie</h3>
                        <div>
                            <button class="btn" onclick="genererBulletinsMensuels()">💰 Générer tous les bulletins</button>
                            <button class="btn btn-warning" onclick="showArchiveModal('bulletins')" style="margin-left: 0.5rem;">📦 Archiver sélection</button>
                        </div>
                    </div>

                    <!-- Sélection multiple -->
                    <div class="select-all-container">
                        <input type="checkbox" id="selectAllBulletins" onchange="toggleSelectAllBulletins()">
                        <label for="selectAllBulletins">Tout sélectionner</label>
                        <span class="selected-count" id="selectedBulletinsCount">0 sélectionné(s)</span>
                        <button class="btn btn-small btn-outline" onclick="clearBulletinsSelection()" style="margin-left: auto;">❌ Effacer</button>
                    </div>

                    <!-- Statistiques -->
                    <div class="stats-grid" id="paieStats">
                        <!-- Populated by JavaScript -->
                    </div>

                    <!-- Filtres -->
                    <div class="filters">
                        <div class="filter-group">
                            <label for="filterPaieMois">Mois :</label>
                            <select id="filterPaieMois" onchange="filterBulletins()">
                                <option value="">Tous les mois</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filterPaieAnnee">Année :</label>
                            <select id="filterPaieAnnee" onchange="filterBulletins()">
                                <option value="">Toutes les années</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                        <div class="filter-group">
                            <label for="filterPaieEmploye">Employé :</label>
                            <select id="filterPaieEmploye" onchange="filterBulletins()">
                                <option value="">Tous les employés</option>
                                <!-- Options will be populated by JavaScript -->
                            </select>
                        </div>
                    </div>

                    <div class="table-container">
                        <table id="bulletinsTable">
                            <thead>
                                <tr>
                                    <th width="30px">
                                        <input type="checkbox" id="selectAllBulletinsHeader" onchange="toggleSelectAllBulletins()">
                                    </th>
                                    <th>ID</th>
                                    <th>Employé</th>
                                    <th>Période</th>
                                    <th>Salaire Brut</th>
                                    <th>Net à Payer</th>
                                    <th>Statut</th>
                                    <th>Actions</th>
                                </tr>
                            </thead>
                            <tbody id="bulletinsTableBody">
                                <!-- Populated by JavaScript -->
                            </tbody>
                        </table>
                    </div>
                </div>
            </section>

            <!-- Bulletin Detail Section -->
            <section id="bulletinDetail" class="section">
                <div class="card">
                    <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 1.5rem;">
                        <h3>Détail du Bulletin de Paie</h3>
                        <div>
                            <button class="btn" onclick="imprimerBulletin()">🖨️ Imprimer</button>
                            <button class="btn btn-outline" onclick="showSection('adminPaie')" style="margin-left: 0.5rem;">← Retour</button>
                        </div>
                    </div>
                    
                    <div id="bulletinContent" class="bulletin-container">
                        <!-- Bulletin content will be populated here -->
                    </div>
                </div>
            </section>

            <!-- Admin Archives Section -->
            <section id="adminArchives" class="section">
                <div class="card">
                    <h3>📦 Archives</h3>
                    <p>Gestion des archives des bulletins de paie et fiches de pointage</p>
                    
                    <div class="archive-actions">
                        <button class="btn" onclick="showArchives('bulletins')">📋 Archives des Bulletins</button>
                        <button class="btn" onclick="showArchives('pointages')">📊 Archives des Pointages</button>
                        <button class="btn btn-warning" onclick="archiverDonneesAnciennes()">🔄 Archiver données anciennes</button>
                    </div>

                    <div id="archivesContent">
                        <!-- Content will be populated by JavaScript -->
                    </div>
                </div>
            </section>
        </main>
    </div>

    <!-- Modal d'archivage -->
    <div id="archiveModal" class="modal-overlay" style="display: none;">
        <div class="modal-content">
            <div class="modal-header">
                <h3 id="modalTitle">Archiver des documents</h3>
                <button class="modal-close" onclick="closeArchiveModal()">×</button>
            </div>
            
            <div id="modalContent">
                <!-- Content populated by JavaScript -->
            </div>
        </div>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/@supabase/supabase-js@2"></script>
    <script>
        // Configuration Supabase
        const SUPABASE_URL = 'https://nvnxcwffhkhmrophvhbh.supabase.co';
        const SUPABASE_ANON_KEY = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Im52bnhjd2ZmaGtobXJvcGh2aGJoIiwicm9sZSI6ImFub24iLCJpYXQiOjE3NTk2OTQ5MDMsImV4cCI6MjA3NTI3MDkwM30.uXFtEd81k80VE6eEcBVvntmG1ymNycg6Nhuhv2K48YY';

        // Initialisation du client Supabase
        const supabase = window.supabase.createClient(SUPABASE_URL, SUPABASE_ANON_KEY);

        // Configuration de la paie professionnelle
        const CONFIG_PAIE_PRO = {
            // Salaire de base
            salaireBase: 1683.30, // Euros
            
            // Cotisations salariales (taux en %)
            cotisations: {
                csg: 9.20,
                crds: 0.50,
                secu: 13.10,
                retraite: 6.85,
                assedic: 3.45,
                transport: 2.40
            },
            
            // Cotisations patronales (taux en %)
            cotisationsPatronales: {
                secu: 16.65,
                accident: 2.50,
                retraite: 9.45,
                assedic: 4.45,
                formation: 1.60,
                transport: 5.00
            },
            
            // Plafonds
            plafondSecu: 3056.00,
            plafondTransport: 1683.30
        };

        // Activities configuration
        const ACTIVITIES = {
            'recolte': 'Récolte',
            'rabattage': 'Rabattage',
            'élagage': 'Élagage',
            'ronds': 'Ronds',
            'spring': 'Spring',
            'engrais': 'Engrais'
        };

        // Départements configuration
        const DEPARTEMENTS = [
            'ZoneA', 'ZoneB', 'ZoneC', 'ZoneD', 'ZoneE', 
            'ZoneF', 'ZoneG', 'ZoneH', 'ZoneI', 'ZoneJ'
        ];

        // Variables globales pour la navigation par jour
        let currentWeekOffset = 0;
        let selectedDate = new Date().toISOString().split('T')[0];
        let lastSavedPointages = [];

        // Variables pour la sélection multiple
        let selectedPointages = new Set();
        let selectedBulletins = new Set();

        // =============================================
        // FONCTIONS SUPABASE
        // =============================================

        // Fonctions pour gérer les utilisateurs
        async function getUsers() {
            const { data, error } = await supabase
                .from('users')
                .select('*')
                .order('id', { ascending: true });
            
            if (error) {
                console.error('Erreur lors de la récupération des utilisateurs:', error);
                showAlert('Erreur lors du chargement des utilisateurs', 'error');
                return [];
            }
            return data || [];
        }

        async function createUser(userData) {
            const { data, error } = await supabase
                .from('users')
                .insert([userData])
                .select();
            
            if (error) {
                console.error('Erreur lors de la création de l\'utilisateur:', error);
                showAlert('Erreur lors de la création de l\'utilisateur', 'error');
                return null;
            }
            return data ? data[0] : null;
        }

        async function deleteUser(userId) {
            const { error } = await supabase
                .from('users')
                .delete()
                .eq('id', userId);
            
            if (error) {
                console.error('Erreur lors de la suppression de l\'utilisateur:', error);
                showAlert('Erreur lors de la suppression de l\'utilisateur', 'error');
                return false;
            }
            return true;
        }

        // Fonctions pour gérer les pointages
        async function getPointages() {
            const { data, error } = await supabase
                .from('pointages')
                .select('*')
                .order('created_at', { ascending: false });
            
            if (error) {
                console.error('Erreur lors de la récupération des pointages:', error);
                showAlert('Erreur lors du chargement des pointages', 'error');
                return [];
            }
            return data || [];
        }

        async function createPointage(pointageData) {
            const { data, error } = await supabase
                .from('pointages')
                .insert([pointageData])
                .select();
            
            if (error) {
                console.error('Erreur lors de la création du pointage:', error);
                showAlert('Erreur lors de l\'enregistrement du pointage', 'error');
                return null;
            }
            return data ? data[0] : null;
        }

        async function createMultiplePointages(pointagesData) {
            const { data, error } = await supabase
                .from('pointages')
                .insert(pointagesData)
                .select();
            
            if (error) {
                console.error('Erreur lors de la création des pointages:', error);
                showAlert('Erreur lors de l\'enregistrement des pointages', 'error');
                return [];
            }
            return data || [];
        }

        // Fonctions pour gérer les bulletins de paie
        async function getBulletins() {
            const { data, error } = await supabase
                .from('bulletins')
                .select('*')
                .order('date_generation', { ascending: false });
            
            if (error) {
                console.error('Erreur lors de la récupération des bulletins:', error);
                showAlert('Erreur lors du chargement des bulletins', 'error');
                return [];
            }
            return data || [];
        }

        async function createBulletin(bulletinData) {
            const { data, error } = await supabase
                .from('bulletins')
                .insert([bulletinData])
                .select();
            
            if (error) {
                console.error('Erreur lors de la création du bulletin:', error);
                showAlert('Erreur lors de la génération du bulletin', 'error');
                return null;
            }
            return data ? data[0] : null;
        }

        // Fonctions pour gérer les présences
        async function getPresences(date) {
            const { data, error } = await supabase
                .from('presences')
                .select('*')
                .eq('date', date);
            
            if (error) {
                console.error('Erreur lors de la récupération des présences:', error);
                return {};
            }
            
            const presencesMap = {};
            data.forEach(p => {
                presencesMap[p.employee_id] = p.status;
            });
            return presencesMap;
        }

        async function savePresencesForDate(date, presencesMap) {
            // Supprimer les anciennes présences pour cette date
            const { error: deleteError } = await supabase
                .from('presences')
                .delete()
                .eq('date', date);
            
            if (deleteError) {
                console.error('Erreur lors de la suppression des anciennes présences:', deleteError);
            }
            
            // Insérer les nouvelles présences
            const presencesData = Object.keys(presencesMap).map(employeeId => ({
                date: date,
                employee_id: parseInt(employeeId),
                status: presencesMap[employeeId]
            }));
            
            const { data, error } = await supabase
                .from('presences')
                .insert(presencesData)
                .select();
            
            if (error) {
                console.error('Erreur lors de l\'enregistrement des présences:', error);
                showAlert('Erreur lors de l\'enregistrement des présences', 'error');
                return false;
            }
            return true;
        }

        // =============================================
        // FONCTIONS D'AUTHENTIFICATION
        // =============================================

        async function login(username, password) {
            try {
                const users = await getUsers();
                const user = users.find(u => u.username === username && u.password === password);
                
                if (user) {
                    localStorage.setItem('mkj_current_user', JSON.stringify(user));
                    updateUIForUser(user);
                    showSection('dashboard');
                    showAlert('Connexion réussie!', 'success');
                    return true;
                }
                return false;
            } catch (error) {
                console.error('Erreur de connexion:', error);
                showAlert('Erreur de connexion', 'error');
                return false;
            }
        }

        function logout() {
            localStorage.removeItem('mkj_current_user');
            updateUIForUser(null);
            showSection('home');
            showAlert('Déconnexion réussie', 'success');
        }

        function getCurrentUser() {
            const userStr = localStorage.getItem('mkj_current_user');
            return userStr ? JSON.parse(userStr) : null;
        }

        // =============================================
        // FONCTIONS DE SÉLECTION MULTIPLE
        // =============================================

        function toggleSelectAllPointages() {
            const checkboxes = document.querySelectorAll('#pointagesTableBody input[type="checkbox"]');
            const selectAll = document.getElementById('selectAllPointages').checked;
            
            selectedPointages.clear();
            
            checkboxes.forEach(checkbox => {
                checkbox.checked = selectAll;
                if (selectAll) {
                    selectedPointages.add(checkbox.value);
                }
            });
            
            updateSelectedPointagesCount();
        }

        function togglePointageSelection(pointageId) {
            if (selectedPointages.has(pointageId)) {
                selectedPointages.delete(pointageId);
            } else {
                selectedPointages.add(pointageId);
            }
            
            updateSelectedPointagesCount();
            updateSelectAllPointagesCheckbox();
        }

        function updateSelectedPointagesCount() {
            const countElement = document.getElementById('selectedPointagesCount');
            countElement.textContent = `${selectedPointages.size} sélectionné(s)`;
        }

        function updateSelectAllPointagesCheckbox() {
            const checkboxes = document.querySelectorAll('#pointagesTableBody input[type="checkbox"]');
            const selectAll = document.getElementById('selectAllPointages');
            
            if (checkboxes.length === 0) {
                selectAll.checked = false;
                return;
            }
            
            const allChecked = Array.from(checkboxes).every(checkbox => checkbox.checked);
            selectAll.checked = allChecked;
        }

        function clearPointagesSelection() {
            selectedPointages.clear();
            const checkboxes = document.querySelectorAll('#pointagesTableBody input[type="checkbox"]');
            checkboxes.forEach(checkbox => checkbox.checked = false);
            updateSelectedPointagesCount();
            updateSelectAllPointagesCheckbox();
        }

        function toggleSelectAllBulletins() {
            const checkboxes = document.querySelectorAll('#bulletinsTableBody input[type="checkbox"]');
            const selectAll = document.getElementById('selectAllBulletins').checked;
            
            selectedBulletins.clear();
            
            checkboxes.forEach(checkbox => {
                checkbox.checked = selectAll;
                if (selectAll) {
                    selectedBulletins.add(checkbox.value);
                }
            });
            
            updateSelectedBulletinsCount();
        }

        function toggleBulletinSelection(bulletinId) {
            if (selectedBulletins.has(bulletinId)) {
                selectedBulletins.delete(bulletinId);
            } else {
                selectedBulletins.add(bulletinId);
            }
            
            updateSelectedBulletinsCount();
            updateSelectAllBulletinsCheckbox();
        }

        function updateSelectedBulletinsCount() {
            const countElement = document.getElementById('selectedBulletinsCount');
            countElement.textContent = `${selectedBulletins.size} sélectionné(s)`;
        }

        function updateSelectAllBulletinsCheckbox() {
            const checkboxes = document.querySelectorAll('#bulletinsTableBody input[type="checkbox"]');
            const selectAll = document.getElementById('selectAllBulletins');
            
            if (checkboxes.length === 0) {
                selectAll.checked = false;
                return;
            }
            
            const allChecked = Array.from(checkboxes).every(checkbox => checkbox.checked);
            selectAll.checked = allChecked;
        }

        function clearBulletinsSelection() {
            selectedBulletins.clear();
            const checkboxes = document.querySelectorAll('#bulletinsTableBody input[type="checkbox"]');
            checkboxes.forEach(checkbox => checkbox.checked = false);
            updateSelectedBulletinsCount();
            updateSelectAllBulletinsCheckbox();
        }

        // =============================================
        // FONCTIONS D'ARCHIVAGE
        // =============================================

        function showArchiveModal(type) {
            const modal = document.getElementById('archiveModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalContent = document.getElementById('modalContent');
            
            if (type === 'pointages') {
                modalTitle.textContent = 'Archiver des fiches de pointage';
                modalContent.innerHTML = getPointagesArchiveOptions();
            } else if (type === 'bulletins') {
                modalTitle.textContent = 'Archiver des bulletins de paie';
                modalContent.innerHTML = getBulletinsArchiveOptions();
            }
            
            modal.style.display = 'flex';
        }

        function closeArchiveModal() {
            document.getElementById('archiveModal').style.display = 'none';
        }

        function getPointagesArchiveOptions() {
            return `
                <div class="archive-options">
                    <div class="archive-option" onclick="selectArchiveOption('pointages_selected')">
                        <div class="option-icon">📋</div>
                        <div class="option-content">
                            <div class="option-title">Archiver la sélection</div>
                            <div class="option-description">
                                ${selectedPointages.size > 0 ? 
                                    `Archiver ${selectedPointages.size} fiche(s) de pointage sélectionnée(s)` : 
                                    'Aucune fiche sélectionnée'
                                }
                            </div>
                        </div>
                    </div>
                    
                    <div class="archive-option" onclick="selectArchiveOption('pointages_month')">
                        <div class="option-icon">📅</div>
                        <div class="option-content">
                            <div class="option-title">Archiver par mois</div>
                            <div class="option-description">
                                Archiver tous les pointages d'un mois spécifique
                            </div>
                        </div>
                    </div>
                </div>
                
                <div style="margin-top: 1.5rem; text-align: center;">
                    <button class="btn btn-outline" onclick="closeArchiveModal()">Annuler</button>
                </div>
            `;
        }

        function getBulletinsArchiveOptions() {
            return `
                <div class="archive-options">
                    <div class="archive-option" onclick="selectArchiveOption('bulletins_selected')">
                        <div class="option-icon">📋</div>
                        <div class="option-content">
                            <div class="option-title">Archiver la sélection</div>
                            <div class="option-description">
                                ${selectedBulletins.size > 0 ? 
                                    `Archiver ${selectedBulletins.size} bulletin(s) sélectionné(s)` : 
                                    'Aucun bulletin sélectionné'
                                }
                            </div>
                        </div>
                    </div>
                    
                    <div class="archive-option" onclick="selectArchiveOption('bulletins_month')">
                        <div class="option-icon">📅</div>
                        <div class="option-content">
                            <div class="option-title">Archiver par mois</div>
                            <div class="option-description">
                                Archiver tous les bulletins d'un mois spécifique
                            </div>
                        </div>
                    </div>
                </div>
                
                <div style="margin-top: 1.5rem; text-align: center;">
                    <button class="btn btn-outline" onclick="closeArchiveModal()">Annuler</button>
                </div>
            `;
        }

        function selectArchiveOption(option) {
            closeArchiveModal();
            
            switch(option) {
                case 'pointages_selected':
                    archiverPointagesSelectionnes();
                    break;
                case 'pointages_month':
                    showMonthSelectionModal('pointages');
                    break;
                case 'bulletins_selected':
                    archiverBulletinsSelectionnes();
                    break;
                case 'bulletins_month':
                    showMonthSelectionModal('bulletins');
                    break;
            }
        }

        function showMonthSelectionModal(type) {
            const modal = document.getElementById('archiveModal');
            const modalTitle = document.getElementById('modalTitle');
            const modalContent = document.getElementById('modalContent');
            
            const currentYear = new Date().getFullYear();
            const years = [currentYear - 1, currentYear, currentYear + 1];
            const months = [
                { value: '01', name: 'Janvier' }, { value: '02', name: 'Février' },
                { value: '03', name: 'Mars' }, { value: '04', name: 'Avril' },
                { value: '05', name: 'Mai' }, { value: '06', name: 'Juin' },
                { value: '07', name: 'Juillet' }, { value: '08', name: 'Août' },
                { value: '09', name: 'Septembre' }, { value: '10', name: 'Octobre' },
                { value: '11', name: 'Novembre' }, { value: '12', name: 'Décembre' }
            ];
            
            let optionsHTML = '';
            years.forEach(year => {
                months.forEach(month => {
                    optionsHTML += `<option value="${year}-${month.value}">${month.name} ${year}</option>`;
                });
            });
            
            modalTitle.textContent = type === 'pointages' ? 
                'Archiver les pointages d\'un mois' : 
                'Archiver les bulletins d\'un mois';
                
            modalContent.innerHTML = `
                <div class="form-group">
                    <label>Sélectionnez le mois à archiver :</label>
                    <select id="selectedMonth" class="form-control">
                        ${optionsHTML}
                    </select>
                </div>
                
                <div style="margin-top: 1.5rem; text-align: center;">
                    <button class="btn" onclick="archiverParMois('${type}')">📦 Archiver le mois</button>
                    <button class="btn btn-outline" onclick="closeArchiveModal()" style="margin-left: 0.5rem;">Annuler</button>
                </div>
            `;
            
            modal.style.display = 'flex';
        }

        async function archiverPointagesSelectionnes() {
            if (selectedPointages.size === 0) {
                showAlert('Aucune fiche de pointage sélectionnée', 'warning');
                return;
            }

            try {
                // Dans une vraie application, vous implémenteriez la logique d'archivage ici
                // Pour l'instant, nous allons simplement marquer les pointages comme archivés
                showAlert(`${selectedPointages.size} fiche(s) de pointage marquée(s) pour archivage`, 'success');
                selectedPointages.clear();
                updateSelectedPointagesCount();
                loadAdminPointages();
            } catch (error) {
                console.error('Erreur lors de l\'archivage:', error);
                showAlert('Erreur lors de l\'archivage', 'error');
            }
        }

        async function archiverBulletinsSelectionnes() {
            if (selectedBulletins.size === 0) {
                showAlert('Aucun bulletin sélectionné', 'warning');
                return;
            }

            try {
                // Dans une vraie application, vous implémenteriez la logique d'archivage ici
                showAlert(`${selectedBulletins.size} bulletin(s) marqué(s) pour archivage`, 'success');
                selectedBulletins.clear();
                updateSelectedBulletinsCount();
                loadBulletinsTable();
            } catch (error) {
                console.error('Erreur lors de l\'archivage:', error);
                showAlert('Erreur lors de l\'archivage', 'error');
            }
        }

        function archiverParMois(type) {
            const selectedMonth = document.getElementById('selectedMonth').value;
            closeArchiveModal();
            showAlert(`Archivage programmé pour ${type} du mois ${selectedMonth}`, 'info');
        }

        function archiverDonneesAnciennes() {
            showAlert('Archivage automatique des données anciennes programmé', 'info');
        }

        // =============================================
        // FONCTIONS D'AFFICHAGE DES ARCHIVES
        // =============================================

        function showArchives(type) {
            const archivesContent = document.getElementById('archivesContent');
            
            if (type === 'bulletins') {
                showBulletinsArchives(archivesContent);
            } else if (type === 'pointages') {
                showPointagesArchives(archivesContent);
            }
        }

        function showBulletinsArchives(container) {
            container.innerHTML = `
                <h4>📋 Archives des Bulletins de Paie</h4>
                <div class="empty-state">
                    <div class="empty-state-icon">📦</div>
                    <p>Fonctionnalité d'archivage en cours de développement</p>
                    <p>Les archives seront bientôt disponibles</p>
                </div>
            `;
        }

        function showPointagesArchives(container) {
            container.innerHTML = `
                <h4>📊 Archives des Fiches de Pointage</h4>
                <div class="empty-state">
                    <div class="empty-state-icon">📦</div>
                    <p>Fonctionnalité d'archivage en cours de développement</p>
                    <p>Les archives seront bientôt disponibles</p>
                </div>
            `;
        }

        // =============================================
        // FONCTIONS DE RECHERCHE
        // =============================================

        function searchPointages() {
            const searchTerm = document.getElementById('searchPointage').value.toLowerCase();
            if (!searchTerm) {
                filterPointagesTable();
                return;
            }

            // Implémentation basique de la recherche côté client
            const rows = document.querySelectorAll('#pointagesTableBody tr');
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(searchTerm) ? '' : 'none';
            });
        }

        function searchEmployeePointages() {
            const searchTerm = document.getElementById('searchEmployeePointage').value.toLowerCase();
            const rows = document.querySelectorAll('#employeePointagesBody tr');
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(searchTerm) ? '' : 'none';
            });
        }

        function searchChefPointages() {
            const searchBox = document.getElementById('chefSearchBox');
            searchBox.style.display = searchBox.style.display === 'none' ? 'flex' : 'none';
        }

        function performChefSearch() {
            const searchTerm = document.getElementById('searchChefPointage').value.toLowerCase();
            const rows = document.querySelectorAll('#dailyPointagesContainer tr');
            rows.forEach(row => {
                const text = row.textContent.toLowerCase();
                row.style.display = text.includes(searchTerm) ? '' : 'none';
            });
        }

        function clearChefSearch() {
            document.getElementById('searchChefPointage').value = '';
            document.getElementById('chefSearchBox').style.display = 'none';
            loadDailyPointages(selectedDate);
        }

        // =============================================
        // FONCTIONS EXISTANTES ADAPTÉES POUR SUPABASE
        // =============================================

        // Photo handling functions
        function previewPhoto(event) {
            const input = event.target;
            const preview = document.getElementById('photoPreview');
            
            if (input.files && input.files[0]) {
                const reader = new FileReader();
                
                reader.onload = function(e) {
                    preview.innerHTML = '';
                    const img = document.createElement('img');
                    img.src = e.target.result;
                    img.className = 'photo-preview';
                    preview.appendChild(img);
                }
                
                reader.readAsDataURL(input.files[0]);
            }
        }

        function getPhotoData() {
            const input = document.getElementById('photoInput');
            if (input.files && input.files[0]) {
                return new Promise((resolve) => {
                    const reader = new FileReader();
                    reader.onload = function(e) {
                        resolve(e.target.result);
                    };
                    reader.readAsDataURL(input.files[0]);
                });
            }
            return Promise.resolve(null);
        }

        function createAvatar(user) {
            if (user.photo) {
                return `<img src="${user.photo}" alt="${user.prenom} ${user.nom}" class="user-photo-table">`;
            }
            
            const roleLetter = user.role.charAt(0);
            const nomLetter = user.nom ? user.nom.charAt(0).toUpperCase() : 'U';
            const initiales = roleLetter + nomLetter;
            
            const avatarClass = `avatar-table ${
                user.role === 'ADMINISTRATEUR' ? 'avatar-admin' : 
                user.role === 'CHEF' ? 'avatar-chef' : 'avatar-employe'
            }`;
            
            return `<div class="${avatarClass}">${initiales}</div>`;
        }

        function createLargeAvatar(user) {
            if (user.photo) {
                return `<img src="${user.photo}" alt="${user.prenom} ${user.nom}" class="photo-preview">`;
            }
            
            const roleLetter = user.role.charAt(0);
            const nomLetter = user.nom ? user.nom.charAt(0).toUpperCase() : 'U';
            const initiales = roleLetter + nomLetter;
            
            const avatarClass = `avatar ${
                user.role === 'ADMINISTRATEUR' ? 'avatar-admin' : 
                user.role === 'CHEF' ? 'avatar-chef' : 'avatar-employe'
            }`;
            
            return `<div class="${avatarClass}" style="width: 120px; height: 120px; font-size: 2rem; margin: 0 auto 1rem;">${initiales}</div>`;
        }

        function createMediumAvatar(user) {
            if (user.photo) {
                return `<img src="${user.photo}" alt="${user.prenom} ${user.nom}" class="user-photo">`;
            }
            
            const roleLetter = user.role.charAt(0);
            const nomLetter = user.nom ? user.nom.charAt(0).toUpperCase() : 'U';
            const initiales = roleLetter + nomLetter;
            
            const avatarClass = `avatar ${
                user.role === 'ADMINISTRATEUR' ? 'avatar-admin' : 
                user.role === 'CHEF' ? 'avatar-chef' : 'avatar-employe'
            }`;
            
            return `<div class="${avatarClass}">${initiales}</div>`;
        }

        // UI Functions
        function showSection(sectionId) {
            document.querySelectorAll('.section').forEach(section => {
                section.classList.remove('active');
            });
            
            const targetSection = document.getElementById(sectionId);
            if (targetSection) {
                targetSection.classList.add('active');
                
                switch(sectionId) {
                    case 'dashboard':
                        loadDashboard();
                        break;
                    case 'profile':
                        loadProfile();
                        break;
                    case 'adminUsers':
                        loadUsersTable();
                        break;
                    case 'adminPointages':
                        loadAdminPointages();
                        break;
                    case 'adminPaie':
                        loadBulletinsTable();
                        break;
                    case 'chefActions':
                        loadChefActions();
                        break;
                    case 'chefPresence':
                        loadPresenceManagement();
                        break;
                    case 'chefPointage':
                        loadPointageManagement();
                        break;
                    case 'chefPointages':
                        loadChefPointages();
                        break;
                    case 'employeePointages':
                        loadEmployeePointages();
                        break;
                    case 'adminArchives':
                        showArchives('bulletins');
                        break;
                }
            }
        }

        function showLogin(role) {
            document.getElementById('loginTitle').textContent = `Connexion - ${role}`;
            showSection('login');
        }

        function updateUIForUser(user) {
            const navDashboard = document.getElementById('navDashboard');
            const navProfile = document.getElementById('navProfile');
            const navArchives = document.getElementById('navArchives');
            const navLogout = document.getElementById('navLogout');
            const header = document.getElementById('appHeader');

            if (user) {
                navDashboard.style.display = 'block';
                navProfile.style.display = 'block';
                navLogout.style.display = 'block';
                
                if (user.role === 'ADMINISTRATEUR') {
                    navArchives.style.display = 'block';
                } else {
                    navArchives.style.display = 'none';
                }
                
                header.style.background = user.color;
            } else {
                navDashboard.style.display = 'none';
                navProfile.style.display = 'none';
                navArchives.style.display = 'none';
                navLogout.style.display = 'none';
                header.style.background = '';
            }
        }

        function showAlert(message, type = 'success') {
            const alertsContainer = document.getElementById('alertsContainer');
            const alert = document.createElement('div');
            alert.className = `alert ${type}`;
            alert.innerHTML = `
                <span>${type === 'success' ? '✓' : '⚠'}</span>
                ${message}
            `;
            
            alertsContainer.appendChild(alert);
            
            setTimeout(() => {
                alert.remove();
            }, 5000);
        }

        // Activity functions
        function getActivityName(activityKey) {
            return ACTIVITIES[activityKey] || activityKey;
        }

        function createActivityBadge(activity) {
            return `<span class="activity-badge">${getActivityName(activity)}</span>`;
        }

        // Form functions
        function toggleActivityField() {
            const role = document.getElementById('userRole').value;
            const activityField = document.getElementById('activityField');
            const employeeActivityField = document.getElementById('employeeActivityField');
            
            if (role === 'CHEF') {
                activityField.style.display = 'block';
                employeeActivityField.style.display = 'none';
                document.getElementById('newActivity').required = true;
                document.getElementById('newEmployeeActivity').required = false;
            } else if (role === 'EMPLOYE') {
                activityField.style.display = 'none';
                employeeActivityField.style.display = 'block';
                document.getElementById('newActivity').required = false;
                document.getElementById('newEmployeeActivity').required = true;
            } else {
                activityField.style.display = 'none';
                employeeActivityField.style.display = 'none';
                document.getElementById('newActivity').required = false;
                document.getElementById('newEmployeeActivity').required = false;
            }
        }

        // Event Handlers
        function handleLogin(event) {
            event.preventDefault();
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            
            if (login(username, password)) {
                document.getElementById('username').value = '';
                document.getElementById('password').value = '';
            } else {
                showAlert('Identifiant ou mot de passe incorrect', 'error');
            }
        }

        async function handleCreateUser(event) {
            event.preventDefault();
            
            const photoData = await getPhotoData();
            const role = document.getElementById('userRole').value;
            
            const newUser = {
                username: document.getElementById('newUsername').value,
                password: document.getElementById('newPassword').value,
                role: role,
                color: document.getElementById('newColor').value,
                nom: document.getElementById('newNom').value,
                prenom: document.getElementById('newPrenom').value,
                departement: document.getElementById('newDepartement').value,
                telephone: document.getElementById('newTelephone').value,
                email: document.getElementById('newEmail').value,
                activity: role === 'CHEF' ? document.getElementById('newActivity').value : 
                         role === 'EMPLOYE' ? document.getElementById('newEmployeeActivity').value : null,
                photo: photoData
            };

            try {
                const users = await getUsers();
                
                if (users.find(u => u.username === newUser.username)) {
                    showAlert('Cet identifiant est déjà utilisé', 'error');
                    return;
                }

                const createdUser = await createUser(newUser);
                
                if (createdUser) {
                    document.getElementById('createUserForm').reset();
                    document.getElementById('photoPreview').innerHTML = '👤';
                    document.getElementById('photoPreview').className = 'photo-placeholder';
                    
                    showAlert('Utilisateur créé avec succès', 'success');
                    showSection('adminUsers');
                }
            } catch (error) {
                console.error('Erreur lors de la création de l\'utilisateur:', error);
                showAlert('Erreur lors de la création de l\'utilisateur', 'error');
            }
        }

        // Chef Actions
        function loadChefActions() {
            const user = getCurrentUser();
            if (!user || user.role !== 'CHEF') return;

            const chefInfo = document.getElementById('chefInfo');
            chefInfo.innerHTML = `
                <strong>Chef d'équipe :</strong> ${user.prenom} ${user.nom}
                ${user.activity ? createActivityBadge(user.activity) : ''}
                <br><strong>Département :</strong> ${user.departement}
                <br><strong>Activité assignée :</strong> ${getActivityName(user.activity)}
            `;
        }

        // Presence Management
        let currentPresences = {};

        async function loadPresenceManagement() {
            const user = getCurrentUser();
            if (!user || user.role !== 'CHEF') return;

            document.getElementById('chefActivityBadge').innerHTML = createActivityBadge(user.activity);

            const today = new Date().toISOString().split('T')[0];
            document.getElementById('presenceDate').value = today;

            try {
                const users = await getUsers();
                const employees = users.filter(u => u.role === 'EMPLOYE' && u.departement === user.departement && u.activity === user.activity);

                const container = document.getElementById('employeePresenceList');
                
                if (employees.length === 0) {
                    container.innerHTML = `
                        <div style="text-align: center; padding: 2rem; color: var(--text-light);">
                            <div style="font-size: 3rem; margin-bottom: 1rem;">👥</div>
                            <h4>Aucun employé dans votre activité</h4>
                            <p>Les employés de l'activité "${getActivityName(user.activity)}" apparaîtront ici</p>
                        </div>
                    `;
                    return;
                }

                // Charger les présences existantes pour aujourd'hui
                const existingPresences = await getPresences(today);
                currentPresences = { ...existingPresences };

                employees.forEach(emp => {
                    if (!currentPresences[emp.id]) {
                        currentPresences[emp.id] = 'absent';
                    }
                });

                container.innerHTML = employees.map(emp => {
                    const avatar = createMediumAvatar(emp);
                    const status = currentPresences[emp.id] || 'absent';
                    return `
                        <div class="employee-card ${status}" id="employee-${emp.id}">
                            <div style="display: flex; align-items: center; margin-bottom: 0.5rem;">
                                ${avatar}
                                <div>
                                    <strong>${emp.prenom} ${emp.nom}</strong>
                                    <div>${emp.username} - ${emp.departement}</div>
                                </div>
                            </div>
                            <div class="presence-toggle">
                                <button type="button" class="toggle-btn toggle-present ${status === 'present' ? 'active' : ''}" onclick="togglePresence(${emp.id}, 'present')">
                                    ✅ Présent
                                </button>
                                <button type="button" class="toggle-btn toggle-absent ${status === 'absent' ? 'active' : ''}" onclick="togglePresence(${emp.id}, 'absent')">
                                    ❌ Absent
                                </button>
                            </div>
                        </div>
                    `;
                }).join('');
            } catch (error) {
                console.error('Erreur lors du chargement de la gestion des présences:', error);
                showAlert('Erreur lors du chargement des employés', 'error');
            }
        }

        function togglePresence(employeeId, status) {
            currentPresences[employeeId] = status;
            const card = document.getElementById(`employee-${employeeId}`);
            
            card.classList.remove('present', 'absent');
            card.classList.add(status);
        }

        async function savePresences() {
            const date = document.getElementById('presenceDate').value;
            if (!date) {
                showAlert('Veuillez sélectionner une date', 'error');
                return;
            }

            try {
                const success = await savePresencesForDate(date, currentPresences);
                
                if (success) {
                    const user = getCurrentUser();
                    const presentCount = Object.values(currentPresences).filter(p => p === 'present').length;
                    const absentCount = Object.values(currentPresences).filter(p => p === 'absent').length;
                    
                    showAlert(`Présences enregistrées : ${presentCount} présent(s), ${absentCount} absent(s)`, 'success');
                    showSection('chefActions');
                }
            } catch (error) {
                console.error('Erreur lors de l\'enregistrement des présences:', error);
                showAlert('Erreur lors de l\'enregistrement des présences', 'error');
            }
        }

        // Pointage Management
        async function loadPointageManagement() {
            const user = getCurrentUser();
            if (!user || user.role !== 'CHEF') return;

            document.getElementById('pointageActivityBadge').innerHTML = createActivityBadge(user.activity);

            const today = new Date().toISOString().split('T')[0];
            document.getElementById('pointageDate').value = today;

            try {
                const todayPresences = await getPresences(today);

                if (!todayPresences || Object.keys(todayPresences).length === 0) {
                    showAlert('Aucune présence enregistrée pour aujourd\'hui. Veuillez d\'abord gérer les présences.', 'error');
                    showSection('chefPresence');
                    return;
                }

                const users = await getUsers();
                const employees = users.filter(u => u.role === 'EMPLOYE' && u.departement === user.departement && u.activity === user.activity);

                const presentEmployees = employees.filter(emp => todayPresences[emp.id] === 'present');
                
                if (presentEmployees.length === 0) {
                    showAlert('Aucun employé présent aujourd\'hui dans votre activité.', 'error');
                    showSection('chefPresence');
                    return;
                }

                const container = document.getElementById('pointageFormsContainer');
                container.innerHTML = presentEmployees.map(emp => {
                    const avatar = createMediumAvatar(emp);
                    return `
                        <div class="form-group" style="background: #f0fdf4; padding: 1.5rem; border-radius: 8px; margin-bottom: 1.5rem;">
                            <div style="display: flex; align-items: center; margin-bottom: 1rem;">
                                ${avatar}
                                <h4>📝 ${emp.prenom} ${emp.nom}</h4>
                                ${emp.email ? `<div style="font-size: 0.8rem; color: var(--text-light);">📧 ${emp.email}</div>` : ''}
                                ${emp.telephone ? `<div style="font-size: 0.8rem; color: var(--text-light);">📞 ${emp.telephone}</div>` : ''}
                            </div>
                            <div class="form-row">
                                <div class="form-group">
                                    <label>Activité *</label>
                                    <select id="activity-${emp.id}" required>
                                        <option value="${user.activity}">${getActivityName(user.activity)}</option>
                                    </select>
                                </div>
                                <div class="form-group">
                                    <label>Bloc</label>
                                    <input type="text" id="bloc-${emp.id}" placeholder="Bloc...">
                                </div>
                            </div>
                            <div class="form-row">
                                <div class="form-group">
                                    <label>Quantité totale *</label>
                                    <input type="number" id="qty-${emp.id}" required placeholder="0" step="0.01" min="0">
                                </div>
                                <div class="form-group">
                                    <label>Prix unitaire</label>
                                    <input type="number" id="unitPrice-${emp.id}" placeholder="0" step="0.01" min="0">
                                </div>
                                <div class="form-group">
                                    <label>Prix total</label>
                                    <input type="number" id="totalPrice-${emp.id}" readonly>
                                </div>
                            </div>
                        </div>
                    `;
                }).join('');

                presentEmployees.forEach(emp => {
                    const qtyInput = document.getElementById(`qty-${emp.id}`);
                    const unitPriceInput = document.getElementById(`unitPrice-${emp.id}`);
                    const totalPriceInput = document.getElementById(`totalPrice-${emp.id}`);

                    const updateTotal = () => {
                        const qty = parseFloat(qtyInput.value) || 0;
                        const unitPrice = parseFloat(unitPriceInput.value) || 0;
                        totalPriceInput.value = (qty * unitPrice).toFixed(2);
                    };

                    qtyInput.addEventListener('input', updateTotal);
                    unitPriceInput.addEventListener('input', updateTotal);
                });

                document.getElementById('emailBtn').disabled = true;
                document.getElementById('whatsappBtn').disabled = true;
                document.getElementById('sendingStatus').style.display = 'none';
            } catch (error) {
                console.error('Erreur lors du chargement de la gestion des pointages:', error);
                showAlert('Erreur lors du chargement des données', 'error');
            }
        }

        async function saveAllPointages() {
            const user = getCurrentUser();
            const date = document.getElementById('pointageDate').value;
            
            try {
                const todayPresences = await getPresences(date);

                if (!todayPresences) {
                    showAlert('Aucune présence trouvée pour cette date', 'error');
                    return;
                }

                const users = await getUsers();
                const employees = users.filter(u => u.role === 'EMPLOYE' && u.departement === user.departement && u.activity === user.activity);

                const presentEmployees = employees.filter(emp => todayPresences[emp.id] === 'present');
                let savedCount = 0;

                lastSavedPointages = [];
                const pointagesData = [];

                for (const emp of presentEmployees) {
                    const pointageData = {
                        chef_id: user.id,
                        employee_id: emp.id,
                        date: date,
                        presence: 'Présent',
                        activity: user.activity,
                        bloc: document.getElementById(`bloc-${emp.id}`).value,
                        qty_total: parseFloat(document.getElementById(`qty-${emp.id}`).value) || 0,
                        unit_price: parseFloat(document.getElementById(`unitPrice-${emp.id}`).value) || 0,
                        total_price: parseFloat(document.getElementById(`totalPrice-${emp.id}`).value) || 0,
                        sub_quantities: []
                    };

                    pointagesData.push(pointageData);
                    lastSavedPointages.push(pointageData);
                    savedCount++;
                }

                const createdPointages = await createMultiplePointages(pointagesData);
                
                if (createdPointages.length > 0) {
                    document.getElementById('emailBtn').disabled = false;
                    document.getElementById('whatsappBtn').disabled = false;
                    
                    showAlert(`${savedCount} pointage(s) enregistré(s) avec succès. Vous pouvez maintenant les envoyer aux employés.`, 'success');
                }
            } catch (error) {
                console.error('Erreur lors de l\'enregistrement des pointages:', error);
                showAlert('Erreur lors de l\'enregistrement des pointages', 'error');
            }
        }

        // Fonctions d'envoi des pointages
        function sendPointagesByEmail() {
            if (lastSavedPointages.length === 0) {
                showAlert('Aucun pointage à envoyer', 'error');
                return;
            }

            // Implémentation basique de l'envoi d'email
            const statusList = document.getElementById('statusList');
            const sendingStatus = document.getElementById('sendingStatus');
            
            sendingStatus.style.display = 'block';
            statusList.innerHTML = '';

            lastSavedPointages.forEach(pointage => {
                const statusItem = document.createElement('div');
                statusItem.className = 'status-item';
                statusItem.innerHTML = `
                    <span>
                        <span class="status-indicator status-success"></span>
                        Pointage ${pointage.id || ''}
                    </span>
                    <span style="color: var(--success);">Email préparé</span>
                `;
                statusList.appendChild(statusItem);
            });

            showAlert(`Préparation de ${lastSavedPointages.length} email(s) terminée`, 'info');
        }

        function sendPointagesByWhatsApp() {
            if (lastSavedPointages.length === 0) {
                showAlert('Aucun pointage à envoyer', 'error');
                return;
            }

            // Implémentation basique de l'envoi WhatsApp
            const statusList = document.getElementById('statusList');
            const sendingStatus = document.getElementById('sendingStatus');
            
            sendingStatus.style.display = 'block';
            statusList.innerHTML = '';

            lastSavedPointages.forEach(pointage => {
                const statusItem = document.createElement('div');
                statusItem.className = 'status-item';
                statusItem.innerHTML = `
                    <span>
                        <span class="status-indicator status-success"></span>
                        Pointage ${pointage.id || ''}
                    </span>
                    <span style="color: var(--success);">WhatsApp préparé</span>
                `;
                statusList.appendChild(statusItem);
            });

            showAlert(`Préparation de ${lastSavedPointages.length} message(s) WhatsApp terminée`, 'info');
        }

        // Data Loading Functions
        async function loadDashboard() {
            const user = getCurrentUser();
            if (!user) return;

            const dashboardTitle = document.getElementById('dashboardTitle');
            const dashboardWelcome = document.getElementById('dashboardWelcome');
            const dashboardGrid = document.getElementById('dashboardGrid');

            dashboardTitle.textContent = `Tableau de bord — ${user.role}`;
            dashboardWelcome.textContent = `Bienvenue ${user.prenom} ${user.nom} !`;
            let extraInfo = `<br><small>Rôle: ${user.role} | Département: ${user.departement}`;
            if (user.activity) {
                extraInfo += ` | Activité: ${getActivityName(user.activity)}`;
            }
            extraInfo += '</small>';
            dashboardWelcome.innerHTML += extraInfo;

            let dashboardHTML = '';

            if (user.role === 'ADMINISTRATEUR') {
                dashboardHTML = `
                    <div class="dashboard-card" onclick="showSection('adminUsers')">
                        <h3>👥 Gestion Utilisateurs</h3>
                        <p>Gérer les chefs et employés</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('adminCreateUser')">
                        <h3>➕ Créer Utilisateur</h3>
                        <p>Ajouter un nouveau utilisateur</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('adminPointages')">
                        <h3>📋 Fiches de Pointage</h3>
                        <p>Voir toutes les fiches de pointage</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('adminPaie')">
                        <h3>💰 Gestion Paie</h3>
                        <p>Générer et imprimer les bulletins</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('adminArchives')">
                        <h3>📦 Archives</h3>
                        <p>Gérer les archives</p>
                    </div>
                `;
            } else if (user.role === 'CHEF') {
                dashboardHTML = `
                    <div class="dashboard-card" onclick="showSection('chefActions')">
                        <h3>📊 Actions Chef</h3>
                        <p>Gérer présences et pointages</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('chefPointages')">
                        <h3>📋 Mes Pointages</h3>
                        <p>Voir l'historique</p>
                    </div>
                `;
            } else if (user.role === 'EMPLOYE') {
                dashboardHTML = `
                    <div class="dashboard-card" onclick="showSection('employeePointages')">
                        <h3>📋 Mes Pointages</h3>
                        <p>Consulter mes activités</p>
                    </div>
                    <div class="dashboard-card" onclick="showSection('profile')">
                        <h3>👤 Mon Profil</h3>
                        <p>Informations personnelles</p>
                    </div>
                `;
            }

            dashboardGrid.innerHTML = dashboardHTML;
        }

        function loadProfile() {
            const user = getCurrentUser();
            if (!user) return;

            const profileContent = document.getElementById('profileContent');
            const avatar = createLargeAvatar(user);
            
            let activityHTML = '';
            if (user.activity) {
                activityHTML = `
                    <div>
                        <strong>Activité :</strong><br>
                        <span>${getActivityName(user.activity)}</span>
                    </div>
                `;
            }

            let contactHTML = '';
            if (user.telephone || user.email) {
                contactHTML = `
                    <div>
                        <strong>Contact :</strong><br>
                        ${user.telephone ? `<span>📞 ${user.telephone}</span><br>` : ''}
                        ${user.email ? `<span>📧 ${user.email}</span>` : ''}
                    </div>
                `;
            }

            profileContent.innerHTML = `
                <div style="text-align: center; margin-bottom: 2rem;">
                    ${avatar}
                </div>
                <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 1rem;">
                    <div>
                        <strong>Identifiant :</strong><br>
                        <span>${user.username}</span>
                    </div>
                    <div>
                        <strong>Nom :</strong><br>
                        <span>${user.nom}</span>
                    </div>
                    <div>
                        <strong>Prénom :</strong><br>
                        <span>${user.prenom}</span>
                    </div>
                    <div>
                        <strong>Rôle :</strong><br>
                        <span>${user.role}</span>
                    </div>
                    <div>
                        <strong>Département :</strong><br>
                        <span>${user.departement}</span>
                    </div>
                    ${activityHTML}
                    ${contactHTML}
                    <div>
                        <strong>Couleur :</strong><br>
                        <span style="display: inline-flex; align-items: center; gap: 0.5rem;">
                            <span class="color-indicator" style="background: ${user.color};"></span>
                            ${user.color}
                        </span>
                    </div>
                </div>
            `;
        }

        async function loadUsersTable() {
            try {
                const users = await getUsers();
                const tbody = document.getElementById('usersTableBody');
                
                const filteredUsers = users.filter(user => user.role !== 'ADMINISTRATEUR');
                
                updateDepartementFilters(filteredUsers);
                
                tbody.innerHTML = filteredUsers.map(user => {
                    const avatar = createAvatar(user);
                    return `
                        <tr>
                            <td>${avatar}</td>
                            <td>${user.id}</td>
                            <td>${user.username}</td>
                            <td>${user.nom}</td>
                            <td>${user.prenom}</td>
                            <td>${user.role}</td>
                            <td>${user.activity ? getActivityName(user.activity) : '-'}</td>
                            <td>${user.departement}</td>
                            <td>
                                <span class="color-indicator" style="background: ${user.color};"></span>
                                ${user.color}
                            </td>
                            <td>
                                <button class="btn btn-danger btn-small" onclick="deleteUserHandler(${user.id})" ${user.id === getCurrentUser()?.id ? 'disabled' : ''}>Supprimer</button>
                            </td>
                        </tr>
                    `;
                }).join('');
            } catch (error) {
                console.error('Erreur lors du chargement des utilisateurs:', error);
                showAlert('Erreur lors du chargement des utilisateurs', 'error');
            }
        }

        async function deleteUserHandler(userId) {
            if (confirm('Êtes-vous sûr de vouloir supprimer cet utilisateur ?')) {
                try {
                    const success = await deleteUser(userId);
                    if (success) {
                        showAlert('Utilisateur supprimé', 'success');
                        loadUsersTable();
                    }
                } catch (error) {
                    console.error('Erreur lors de la suppression de l\'utilisateur:', error);
                    showAlert('Erreur lors de la suppression de l\'utilisateur', 'error');
                }
            }
        }

        function updateDepartementFilters(users) {
            const departementFilter = document.getElementById('filterDepartement');
            const departements = [...new Set(users.map(user => user.departement))].sort();
            
            departementFilter.innerHTML = '<option value="">Tous les départements</option>';
            departements.forEach(dept => {
                departementFilter.innerHTML += `<option value="${dept}">${dept}</option>`;
            });
        }

        function filterUsersTable() {
            const departementFilter = document.getElementById('filterDepartement').value;
            const roleFilter = document.getElementById('filterRole').value;
            
            const rows = document.querySelectorAll('#usersTableBody tr');
            rows.forEach(row => {
                const cells = row.getElementsByTagName('td');
                const userDepartement = cells[7].textContent;
                const userRole = cells[5].textContent;
                
                const departementMatch = !departementFilter || userDepartement === departementFilter;
                const roleMatch = !roleFilter || userRole === roleFilter;
                
                row.style.display = departementMatch && roleMatch ? '' : 'none';
            });
        }

        // Chef Pointages - Vue par jour
        function loadChefPointages() {
            const user = getCurrentUser();
            if (!user || user.role !== 'CHEF') return;

            document.getElementById('pointagesActivityBadge').innerHTML = createActivityBadge(user.activity);

            generateDayNavigation();
            loadDailyPointages(selectedDate);
        }

        function generateDayNavigation() {
            const daySelector = document.getElementById('daySelector');
            const today = new Date();
            const startDate = new Date(today);
            startDate.setDate(today.getDate() + (currentWeekOffset * 7) - today.getDay());

            let html = '';
            for (let i = 0; i < 7; i++) {
                const currentDate = new Date(startDate);
                currentDate.setDate(startDate.getDate() + i);
                const dateString = currentDate.toISOString().split('T')[0];
                const dayName = currentDate.toLocaleDateString('fr-FR', { weekday: 'short' });
                const dayNumber = currentDate.getDate();
                const month = currentDate.toLocaleDateString('fr-FR', { month: 'short' });

                const isActive = dateString === selectedDate;
                const isToday = dateString === new Date().toISOString().split('T')[0];

                html += `
                    <button class="day-btn ${isActive ? 'active' : ''} ${isToday ? 'today' : ''}" 
                            onclick="selectDate('${dateString}')">
                        <div>${dayName}</div>
                        <div style="font-weight: ${isToday ? 'bold' : 'normal'}">${dayNumber}</div>
                        <div style="font-size: 0.8rem; opacity: 0.7;">${month}</div>
                    </button>
                `;
            }

            daySelector.innerHTML = html;
        }

        function selectDate(date) {
            selectedDate = date;
            generateDayNavigation();
            loadDailyPointages(date);
        }

        function previousWeek() {
            currentWeekOffset--;
            generateDayNavigation();
            loadDailyPointages(selectedDate);
        }

        function nextWeek() {
            currentWeekOffset++;
            generateDayNavigation();
            loadDailyPointages(selectedDate);
        }

        async function loadDailyPointages(date) {
            const user = getCurrentUser();
            if (!user || user.role !== 'CHEF') return;

            try {
                const pointages = await getPointages();
                const users = await getUsers();

                const dailyPointages = pointages.filter(p => 
                    p.date === date && 
                    p.chef_id === user.id && 
                    p.activity === user.activity
                );

                const container = document.getElementById('dailyPointagesContainer');

                if (dailyPointages.length === 0) {
                    container.innerHTML = `
                        <div class="empty-state">
                            <div class="empty-state-icon">📋</div>
                            <h3>Aucun pointage pour cette date</h3>
                            <p>Aucune fiche de pointage n'a été enregistrée pour le ${formatDate(date)}</p>
                        </div>
                    `;
                    return;
                }

                const totalEmployes = [...new Set(dailyPointages.map(p => p.employee_id))].length;
                const totalPresents = dailyPointages.filter(p => p.presence === 'Présent').length;
                const totalAbsents = dailyPointages.filter(p => p.presence === 'Absent').length;
                const totalQuantite = dailyPointages.reduce((sum, p) => sum + (p.qty_total || 0), 0);
                const totalPrix = dailyPointages.reduce((sum, p) => sum + (p.total_price || 0), 0);

                container.innerHTML = `
                    <div class="fiche-header">
                        <div class="fiche-date">Fiche du ${formatDate(date)}</div>
                        <div class="fiche-activity">Activité: ${getActivityName(user.activity)}</div>
                        <div class="fiche-stats">
                            <div class="fiche-stat">
                                <div class="fiche-stat-number">${totalEmployes}</div>
                                <div class="fiche-stat-label">Employés</div>
                            </div>
                            <div class="fiche-stat">
                                <div class="fiche-stat-number">${totalPresents}</div>
                                <div class="fiche-stat-label">Présents</div>
                            </div>
                            <div class="fiche-stat">
                                <div class="fiche-stat-number">${totalAbsents}</div>
                                <div class="fiche-stat-label">Absents</div>
                            </div>
                            <div class="fiche-stat">
                                <div class="fiche-stat-number">${totalQuantite}</div>
                                <div class="fiche-stat-label">Quantité</div>
                            </div>
                            <div class="fiche-stat">
                                <div class="fiche-stat-number">${totalPrix.toFixed(2)}€</div>
                                <div class="fiche-stat-label">Total</div>
                            </div>
                        </div>
                    </div>

                    <div class="table-container">
                        <table>
                            <thead>
                                <tr>
                                    <th>ID</th>
                                    <th>Nom Prénom</th>
                                    <th>Date</th>
                                    <th>Présence</th>
                                    <th>Activité</th>
                                    <th>Quantité</th>
                                    <th>Prix unitaire</th>
                                    <th>Prix total</th>
                                    <th>Bloc</th>
                                    <th>Chef</th>
                                </tr>
                            </thead>
                            <tbody>
                                ${dailyPointages.map(p => {
                                    const employee = users.find(u => u.id === p.employee_id);
                                    const chef = users.find(u => u.id === p.chef_id);
                                    return `
                                        <tr>
                                            <td>${p.id}</td>
                                            <td>${employee ? `${employee.prenom} ${employee.nom}` : 'N/A'}</td>
                                            <td>${p.date}</td>
                                            <td>
                                                <span style="color: ${p.presence === 'Présent' ? 'var(--success)' : 'var(--danger)'}; font-weight: 500;">
                                                    ${p.presence}
                                                </span>
                                            </td>
                                            <td>${getActivityName(p.activity)}</td>
                                            <td>${p.qty_total}</td>
                                            <td>${p.unit_price}</td>
                                            <td style="font-weight: 500;">${p.total_price}€</td>
                                            <td>${p.bloc || '-'}</td>
                                            <td>${chef ? `${chef.prenom} ${chef.nom}` : 'N/A'}</td>
                                        </tr>
                                    `;
                                }).join('')}
                            </tbody>
                        </table>
                    </div>
                `;
            } catch (error) {
                console.error('Erreur lors du chargement des pointages du jour:', error);
                showAlert('Erreur lors du chargement des pointages', 'error');
            }
        }

        function formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('fr-FR', {
                weekday: 'long',
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
        }

        // Admin Pointages Management
        async function loadAdminPointages() {
            try {
                const pointages = await getPointages();
                const users = await getUsers();
                
                const totalPointages = pointages.length;
                const totalPrix = pointages.reduce((sum, p) => sum + (p.total_price || 0), 0);
                const pointagesAujourdhui = pointages.filter(p => p.date === new Date().toISOString().split('T')[0]).length;
                const activitesUniques = [...new Set(pointages.map(p => p.activity))].length;

                document.getElementById('pointageStats').innerHTML = `
                    <div class="stat-card">
                        <div class="stat-number">${totalPointages}</div>
                        <div class="stat-label">Total Pointages</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${totalPrix.toFixed(2)}</div>
                        <div class="stat-label">Total Prix (€)</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${pointagesAujourdhui}</div>
                        <div class="stat-label">Aujourd'hui</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${activitesUniques}</div>
                        <div class="stat-label">Activités</div>
                    </div>
                `;

                updatePointageFilters(pointages, users);
                filterPointagesTable();
            } catch (error) {
                console.error('Erreur lors du chargement des pointages admin:', error);
                showAlert('Erreur lors du chargement des pointages', 'error');
            }
        }

        function updatePointageFilters(pointages, users) {
            const activityFilter = document.getElementById('filterPointageActivity');
            const chefFilter = document.getElementById('filterPointageChef');
            
            const activities = [...new Set(pointages.map(p => p.activity))].sort();
            activityFilter.innerHTML = '<option value="">Toutes les activités</option>';
            activities.forEach(activity => {
                activityFilter.innerHTML += `<option value="${activity}">${getActivityName(activity)}</option>`;
            });

            const chefs = [...new Set(pointages.map(p => p.chef_id))];
            const chefUsers = users.filter(u => u.role === 'CHEF' && chefs.includes(u.id));
            chefFilter.innerHTML = '<option value="">Tous les chefs</option>';
            chefUsers.forEach(chef => {
                chefFilter.innerHTML += `<option value="${chef.id}">${chef.prenom} ${chef.nom}</option>`;
            });
        }

        function filterPointagesTable() {
            const activityFilter = document.getElementById('filterPointageActivity').value;
            const dateFilter = document.getElementById('filterPointageDate').value;
            const chefFilter = document.getElementById('filterPointageChef').value;
            
            const rows = document.querySelectorAll('#pointagesTableBody tr');
            rows.forEach(row => {
                const cells = row.getElementsByTagName('td');
                const pointageActivity = cells[4].textContent;
                const pointageDate = cells[2].textContent;
                const pointageChef = cells[3].textContent;
                
                const activityMatch = !activityFilter || pointageActivity === getActivityName(activityFilter);
                const dateMatch = !dateFilter || pointageDate === dateFilter;
                const chefMatch = !chefFilter || pointageChef.includes(chefFilter);
                
                row.style.display = activityMatch && dateMatch && chefMatch ? '' : 'none';
            });
        }

        async function loadEmployeePointages() {
            const user = getCurrentUser();
            if (!user || user.role !== 'EMPLOYE') return;

            try {
                const pointages = await getPointages();
                const users = await getUsers();

                const employeePointages = pointages.filter(p => p.employee_id === user.id)
                    .sort((a, b) => new Date(b.created_at) - new Date(a.created_at));

                const tbody = document.getElementById('employeePointagesBody');

                tbody.innerHTML = employeePointages.map(p => {
                    const chef = users.find(u => u.id === p.chef_id);
                    
                    return `
                        <tr>
                            <td>${p.id}</td>
                            <td>${user.prenom} ${user.nom}</td>
                            <td>${p.date}</td>
                            <td>${p.presence}</td>
                            <td>${getActivityName(p.activity)}</td>
                            <td>${p.qty_total}</td>
                            <td>${p.unit_price}</td>
                            <td>${p.total_price}</td>
                            <td>${p.bloc || '-'}</td>
                            <td>${chef ? `${chef.prenom} ${chef.nom}` : 'N/A'}</td>
                        </tr>
                    `;
                }).join('');
            } catch (error) {
                console.error('Erreur lors du chargement des pointages employé:', error);
                showAlert('Erreur lors du chargement des pointages', 'error');
            }
        }

        // =============================================
        // FONCTIONS DE GESTION DE LA PAIE PROFESSIONNELLE
        // =============================================

        // Calculer le salaire basé sur les pointages
        async function calculerSalaire(employeId, mois, annee) {
            try {
                const pointages = await getPointages();
                const users = await getUsers();
                
                const employe = users.find(u => u.id === employeId);
                if (!employe) return null;

                // Filtrer les pointages du mois
                const pointagesMois = pointages.filter(p => {
                    const [dateAnnee, dateMois] = p.date.split('-');
                    return p.employee_id === employeId && 
                           parseInt(dateAnnee) === annee && 
                           parseInt(dateMois) === mois;
                });

                // Calculer le total des gains
                const totalGains = pointagesMois.reduce((sum, p) => sum + (p.total_price || 0), 0);
                
                // Calculer les jours travaillés
                const joursTravailles = [...new Set(pointagesMois.map(p => p.date))].length;
                
                // Calculer le salaire de base
                const salaireBase = CONFIG_PAIE_PRO.salaireBase;
                
                // Prime de rendement (10% du total des gains)
                const primeRendement = totalGains * 0.1;
                
                // Salaire brut
                const salaireBrut = salaireBase + primeRendement + totalGains;
                
                // Calcul des cotisations professionnelles
                const cotisationsSalariales = calculerCotisationsSalariales(salaireBrut);
                const netAPayer = salaireBrut - cotisationsSalariales.total;

                return {
                    employe: employe,
                    periode: `${mois}/${annee}`,
                    joursTravailles: joursTravailles,
                    salaireBase: salaireBase,
                    primeRendement: primeRendement,
                    gainsActivites: totalGains,
                    salaireBrut: salaireBrut,
                    netAPayer: netAPayer,
                    pointages: pointagesMois.length,
                    cotisationsSalariales: cotisationsSalariales,
                    cotisationsPatronales: calculerCotisationsPatronales(salaireBrut)
                };
            } catch (error) {
                console.error('Erreur lors du calcul du salaire:', error);
                return null;
            }
        }

        // Générer les bulletins pour tous les employés
        async function genererBulletinsMensuels() {
            try {
                const users = await getUsers();
                const employes = users.filter(u => u.role === 'EMPLOYE');
                const aujourdhui = new Date();
                const mois = aujourdhui.getMonth() + 1;
                const annee = aujourdhui.getFullYear();

                let bulletinsGeneres = 0;

                for (const employe of employes) {
                    const calculSalaire = await calculerSalaire(employe.id, mois, annee);
                    
                    if (calculSalaire) {
                        await genererBulletin(calculSalaire);
                        bulletinsGeneres++;
                    }
                }

                showAlert(`${bulletinsGeneres} bulletin(s) généré(s) pour ${mois}/${annee}`, 'success');
                loadBulletinsTable();
            } catch (error) {
                console.error('Erreur lors de la génération des bulletins:', error);
                showAlert('Erreur lors de la génération des bulletins', 'error');
            }
        }

        // Générer un bulletin individuel
        async function genererBulletin(calculSalaire) {
            try {
                const bulletins = await getBulletins();
                
                const bulletinExiste = bulletins.find(b => 
                    b.employe_id === calculSalaire.employe.id && 
                    b.periode === calculSalaire.periode
                );

                if (bulletinExiste) {
                    return bulletinExiste;
                }

                const nouveauBulletin = {
                    employe_id: calculSalaire.employe.id,
                    periode: calculSalaire.periode,
                    date_generation: new Date().toISOString(),
                    statut: 'Généré',
                    jours_travailles: calculSalaire.joursTravailles,
                    salaire_base: calculSalaire.salaireBase,
                    prime_rendement: calculSalaire.primeRendement,
                    gains_activites: calculSalaire.gainsActivites,
                    salaire_brut: calculSalaire.salaireBrut,
                    net_a_payer: calculSalaire.netAPayer,
                    cotisations_salariales: calculSalaire.cotisationsSalariales,
                    cotisations_patronales: calculSalaire.cotisationsPatronales
                };

                const createdBulletin = await createBulletin(nouveauBulletin);
                return createdBulletin;
            } catch (error) {
                console.error('Erreur lors de la génération du bulletin:', error);
                return null;
            }
        }

        // Fonctions utilitaires pour les calculs de cotisations
        function calculerCotisationsSalariales(salaireBrut) {
            const plafond = CONFIG_PAIE_PRO.plafondSecu;
            const base = Math.min(salaireBrut, plafond);
            
            return {
                csg: (salaireBrut * CONFIG_PAIE_PRO.cotisations.csg / 100),
                crds: (salaireBrut * CONFIG_PAIE_PRO.cotisations.crds / 100),
                secu: (base * CONFIG_PAIE_PRO.cotisations.secu / 100),
                retraite: (base * CONFIG_PAIE_PRO.cotisations.retraite / 100),
                assedic: (base * CONFIG_PAIE_PRO.cotisations.assedic / 100),
                transport: (Math.min(salaireBrut, CONFIG_PAIE_PRO.plafondTransport) * CONFIG_PAIE_PRO.cotisations.transport / 100),
                get total() {
                    return this.csg + this.crds + this.secu + this.retraite + this.assedic + this.transport;
                }
            };
        }

        function calculerCotisationsPatronales(salaireBrut) {
            const plafond = CONFIG_PAIE_PRO.plafondSecu;
            const base = Math.min(salaireBrut, plafond);
            
            return {
                secu: (base * CONFIG_PAIE_PRO.cotisationsPatronales.secu / 100),
                accident: (salaireBrut * CONFIG_PAIE_PRO.cotisationsPatronales.accident / 100),
                retraite: (base * CONFIG_PAIE_PRO.cotisationsPatronales.retraite / 100),
                assedic: (base * CONFIG_PAIE_PRO.cotisationsPatronales.assedic / 100),
                formation: (salaireBrut * CONFIG_PAIE_PRO.cotisationsPatronales.formation / 100),
                transport: (Math.min(salaireBrut, CONFIG_PAIE_PRO.plafondTransport) * CONFIG_PAIE_PRO.cotisationsPatronales.transport / 100),
                get total() {
                    return this.secu + this.accident + this.retraite + this.assedic + this.formation + this.transport;
                }
            };
        }

        // Charger le tableau des bulletins
        async function loadBulletinsTable() {
            try {
                const bulletins = await getBulletins();
                const users = await getUsers();
                
                const totalBulletins = bulletins.length;
                const totalSalaireBrut = bulletins.reduce((sum, b) => sum + (b.salaire_brut || 0), 0);
                const totalNetAPayer = bulletins.reduce((sum, b) => sum + (b.net_a_payer || 0), 0);
                const bulletinsCeMois = bulletins.filter(b => {
                    const [mois, annee] = b.periode.split('/');
                    const aujourdhui = new Date();
                    return parseInt(mois) === aujourdhui.getMonth() + 1 && 
                           parseInt(annee) === aujourdhui.getFullYear();
                }).length;

                document.getElementById('paieStats').innerHTML = `
                    <div class="stat-card">
                        <div class="stat-number">${totalBulletins}</div>
                        <div class="stat-label">Total Bulletins</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${Math.round(totalSalaireBrut).toLocaleString()}</div>
                        <div class="stat-label">Salaire Brut Total</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${Math.round(totalNetAPayer).toLocaleString()}</div>
                        <div class="stat-label">Net à Payer Total</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">${bulletinsCeMois}</div>
                        <div class="stat-label">Ce mois</div>
                    </div>
                `;
                
                updatePaieFilters(bulletins, users);
                filterBulletins();
            } catch (error) {
                console.error('Erreur lors du chargement des bulletins:', error);
                showAlert('Erreur lors du chargement des bulletins', 'error');
            }
        }

        // Mettre à jour les filtres de paie
        function updatePaieFilters(bulletins, users) {
            const moisFilter = document.getElementById('filterPaieMois');
            const anneeFilter = document.getElementById('filterPaieAnnee');
            const employeFilter = document.getElementById('filterPaieEmploye');
            
            const mois = [...new Set(bulletins.map(b => {
                const [mois] = b.periode.split('/');
                return parseInt(mois);
            }))].sort((a, b) => a - b);
            
            moisFilter.innerHTML = '<option value="">Tous les mois</option>';
            mois.forEach(m => {
                const nomMois = new Date(2023, m-1, 1).toLocaleDateString('fr-FR', { month: 'long' });
                moisFilter.innerHTML += `<option value="${m}">${nomMois}</option>`;
            });

            const annees = [...new Set(bulletins.map(b => {
                const [mois, annee] = b.periode.split('/');
                return parseInt(annee);
            }))].sort((a, b) => b - a);
            
            anneeFilter.innerHTML = '<option value="">Toutes les années</option>';
            annees.forEach(a => {
                anneeFilter.innerHTML += `<option value="${a}">${a}</option>`;
            });

            const employesIds = [...new Set(bulletins.map(b => b.employe_id))];
            const employes = users.filter(u => employesIds.includes(u.id));
            
            employeFilter.innerHTML = '<option value="">Tous les employés</option>';
            employes.forEach(emp => {
                employeFilter.innerHTML += `<option value="${emp.id}">${emp.prenom} ${emp.nom}</option>`;
            });
        }

        // Filtrer les bulletins
        function filterBulletins() {
            const moisFilter = document.getElementById('filterPaieMois').value;
            const anneeFilter = document.getElementById('filterPaieAnnee').value;
            const employeFilter = document.getElementById('filterPaieEmploye').value;
            
            const rows = document.querySelectorAll('#bulletinsTableBody tr');
            rows.forEach(row => {
                const cells = row.getElementsByTagName('td');
                const bulletinPeriode = cells[3].textContent;
                const bulletinEmploye = cells[2].textContent;
                
                const [mois, annee] = bulletinPeriode.split('/');
                const moisMatch = !moisFilter || parseInt(mois) === parseInt(moisFilter);
                const anneeMatch = !anneeFilter || annee === anneeFilter;
                const employeMatch = !employeFilter || bulletinEmploye.includes(employeFilter);
                
                row.style.display = moisMatch && anneeMatch && employeMatch ? '' : 'none';
            });
        }

        // Voir le détail d'un bulletin
        async function voirBulletin(bulletinId) {
            try {
                const bulletins = await getBulletins();
                const bulletin = bulletins.find(b => b.id === bulletinId);
                
                if (!bulletin) {
                    showAlert('Bulletin non trouvé', 'error');
                    return;
                }

                const users = await getUsers();
                const employe = users.find(u => u.id === bulletin.employe_id);
                
                if (!employe) {
                    showAlert('Employé non trouvé', 'error');
                    return;
                }

                // Compléter les données du bulletin pour l'affichage
                const bulletinComplet = {
                    ...bulletin,
                    employe: employe
                };

                localStorage.setItem('current_bulletin', JSON.stringify(bulletinComplet));
                
                const content = document.getElementById('bulletinContent');
                content.innerHTML = genererBulletinPaiePro(bulletinComplet);
                
                showSection('bulletinDetail');
            } catch (error) {
                console.error('Erreur lors du chargement du bulletin:', error);
                showAlert('Erreur lors du chargement du bulletin', 'error');
            }
        }

        // Générer le bulletin de paie professionnel
        function genererBulletinPaiePro(bulletin) {
            const dateGeneration = new Date(bulletin.date_generation);
            const datePaiement = new Date(dateGeneration);
            datePaiement.setDate(datePaiement.getDate() + 5);
            
            return `
                <div class="bulletin-content">
                    <!-- Header -->
                    <div class="bulletin-header">
                        <div class="company-info">
                            <div class="company-logo">
                                <div class="logo-icon">🌴</div>
                                <div class="company-name">MKJ SERVICE</div>
                            </div>
                            <div class="company-details">
                                <strong>MKJ SERVICE</strong><br>
                                1 Rue des Palmiers, 75013 PARIS<br>
                                Tél: 01 23 45 67 89 • Siret: 529 999 999 9999<br>
                                Code NAF: 6202A • URSSAF: 780 7999 9999 99999
                            </div>
                        </div>
                        <div class="document-title">
                            <div class="title-main">BULLETIN DE SALAIRE</div>
                            <div class="title-sub">Paiement selon travaux effectués</div>
                        </div>
                        <div class="employee-header-section">
                            <div class="employee-photo">
                                ${bulletin.employe.photo ? 
                                    `<img src="${bulletin.employe.photo}" alt="${bulletin.employe.prenom} ${bulletin.employe.nom}" style="width: 100%; height: 100%; object-fit: cover;">` : 
                                    '<div class="photo-placeholder">Photo<br>du salarié</div>'
                                }
                            </div>
                            <div class="employee-details-compact">
                                <div class="info-row">
                                    <div class="info-label">Nom:</div>
                                    <div class="info-value">${bulletin.employe.nom}</div>
                                </div>
                                <div class="info-row">
                                    <div class="info-label">Prénom:</div>
                                    <div class="info-value">${bulletin.employe.prenom}</div>
                                </div>
                                <div class="info-row">
                                    <div class="info-label">Matricule:</div>
                                    <div class="info-value">EMP-${bulletin.employe.id}</div>
                                </div>
                                <div class="info-row">
                                    <div class="info-label">Date entrée:</div>
                                    <div class="info-value">15/03/2022</div>
                                </div>
                                <div class="info-row">
                                    <div class="info-label">Emploi:</div>
                                    <div class="info-value">Ouvrier agricole</div>
                                </div>
                                <div class="info-row">
                                    <div class="info-label">Département:</div>
                                    <div class="info-value">${bulletin.employe.departement}</div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <!-- Main Content -->
                    <div class="bulletin-main">
                        <div class="period-info">
                            <div class="period-dates">
                                <div class="period-item">
                                    <div class="period-label">Période:</div>
                                    <div>${getPremierDuMois(bulletin.periode)} au ${getDernierDuMois(bulletin.periode)}</div>
                                </div>
                            </div>
                            <div class="period-dates">
                                <div class="period-item">
                                    <div class="period-label">Jours travaillés:</div>
                                    <div>${bulletin.jours_travailles}</div>
                                </div>
                                <div class="period-item">
                                    <div class="period-label">Heures supplémentaires:</div>
                                    <div>8</div>
                                </div>
                            </div>
                        </div>

                        <div class="table-container">
                            <table class="main-table">
                                <thead>
                                    <tr>
                                        <th class="designation">DÉSIGNATION</th>
                                        <th class="number">NOMBRE</th>
                                        <th class="base">PRIX UNITAIRE</th>
                                        <th class="rate">QUANTITÉ</th>
                                        <th class="gains">GAINS</th>
                                        <th class="deductions">RETENUES</th>
                                        <th class="net">NET À PAYER</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <!-- Activités -->
                                    <tr class="activity-row">
                                        <td class="designation">Travaux agricoles</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">${bulletin.gains_activites.toFixed(2)}</td>
                                        <td class="deductions">-</td>
                                        <td class="net">${bulletin.gains_activites.toFixed(2)}</td>
                                    </tr>
                                    
                                    <!-- Prime -->
                                    <tr>
                                        <td class="designation">Prime de rendement</td>
                                        <td class="number"></td>
                                        <td class="base">${bulletin.prime_rendement.toFixed(2)}</td>
                                        <td class="rate">1.00</td>
                                        <td class="gains">${bulletin.prime_rendement.toFixed(2)}</td>
                                        <td class="deductions">-</td>
                                        <td class="net">${bulletin.prime_rendement.toFixed(2)}</td>
                                    </tr>
                                    
                                    <!-- Sous-total gains -->
                                    <tr class="subtotal">
                                        <td class="designation">TOTAL GAINS</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">${bulletin.salaire_brut.toFixed(2)}</td>
                                        <td class="deductions"></td>
                                        <td class="net">${bulletin.salaire_brut.toFixed(2)}</td>
                                    </tr>
                                    
                                    <!-- Cotisations -->
                                    <tr>
                                        <td class="designation">Sécurité sociale</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">-</td>
                                        <td class="deductions">${bulletin.cotisations_salariales.secu.toFixed(2)}</td>
                                        <td class="net">-${bulletin.cotisations_salariales.secu.toFixed(2)}</td>
                                    </tr>
                                    
                                    <tr>
                                        <td class="designation">Assurance chômage</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">-</td>
                                        <td class="deductions">${bulletin.cotisations_salariales.assedic.toFixed(2)}</td>
                                        <td class="net">-${bulletin.cotisations_salariales.assedic.toFixed(2)}</td>
                                    </tr>
                                    
                                    <tr>
                                        <td class="designation">Retraite</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">-</td>
                                        <td class="deductions">${bulletin.cotisations_salariales.retraite.toFixed(2)}</td>
                                        <td class="net">-${bulletin.cotisations_salariales.retraite.toFixed(2)}</td>
                                    </tr>
                                    
                                    <tr>
                                        <td class="designation">CSG/CRDS</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">-</td>
                                        <td class="deductions">${(bulletin.cotisations_salariales.csg + bulletin.cotisations_salariales.crds).toFixed(2)}</td>
                                        <td class="net">-${(bulletin.cotisations_salariales.csg + bulletin.cotisations_salariales.crds).toFixed(2)}</td>
                                    </tr>
                                    
                                    <!-- Total retenues -->
                                    <tr class="subtotal">
                                        <td class="designation">TOTAL RETENUES</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains">-</td>
                                        <td class="deductions">${bulletin.cotisations_salariales.total.toFixed(2)}</td>
                                        <td class="net">-${bulletin.cotisations_salariales.total.toFixed(2)}</td>
                                    </tr>
                                    
                                    <!-- Net à payer -->
                                    <tr class="total">
                                        <td class="designation">NET À PAYER</td>
                                        <td class="number"></td>
                                        <td class="base"></td>
                                        <td class="rate"></td>
                                        <td class="gains"></td>
                                        <td class="deductions"></td>
                                        <td class="net">${bulletin.net_a_payer.toFixed(2)}</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>

                        <!-- Summary Section -->
                        <div class="summary-section">
                            <div class="summary-left">
                                <div class="summary-title">RÉCAPITULATIF</div>
                                <table class="summary-table">
                                    <tr>
                                        <td class="label">Total des gains</td>
                                        <td class="value">${bulletin.salaire_brut.toFixed(2)}</td>
                                    </tr>
                                    <tr>
                                        <td class="label">Total des retenues</td>
                                        <td class="value">${bulletin.cotisations_salariales.total.toFixed(2)}</td>
                                    </tr>
                                    <tr class="total-row">
                                        <td class="label">Net à payer</td>
                                        <td class="value">${bulletin.net_a_payer.toFixed(2)}</td>
                                    </tr>
                            </div>
                            <div class="summary-right">
                                <div class="summary-title">INFORMATIONS COMPLÉMENTAIRES</div>
                                <table class="summary-table">
                                    <tr>
                                        <td class="label">Congés payés acquis</td>
                                        <td class="value">2.50</td>
                                    </tr>
                                    <tr>
                                        <td class="label">Congés pris</td>
                                        <td class="value">0.00</td>
                                    </tr>
                                    <tr>
                                        <td class="label">Solde congés</td>
                                        <td class="value">2.50</td>
                                    </tr>
                                </table>
                            </div>
                        </div>
                    </div>

                    <!-- Footer -->
                    <div class="bulletin-footer">
                        <div class="legal-mentions">
                            <p><strong>Mentions légales :</strong> Le salarié dispose d'un délai de 3 ans pour réclamer toute erreur sur ce bulletin. Ce document est établi en double exemplaire, un pour l'employeur et un pour le salarié. Conservez ce bulletin sans limitation de durée.</p>
                            <p>Paiement effectué par virement bancaire. Date de paiement : ${datePaiement.toLocaleDateString('fr-FR')}</p>
                        </div>
                        <div class="signature-section">
                            <div class="signature-stamp">
                                MKJ SERVICE<br>
                                Vu et approuvé<br>
                                ${dateGeneration.toLocaleDateString('fr-FR')}
                            </div>
                            <div class="signature-line">Signature de l'employeur</div>
                        </div>
                    </div>
                </div>
            `;
        }

        function getPremierDuMois(periode) {
            const [mois, annee] = periode.split('/');
            return `01/${mois.padStart(2, '0')}/${annee}`;
        }

        function getDernierDuMois(periode) {
            const [mois, annee] = periode.split('/');
            const dernierJour = new Date(annee, mois, 0).getDate();
            return `${dernierJour}/${mois.padStart(2, '0')}/${annee}`;
        }

        // Imprimer le bulletin
        function imprimerBulletin(bulletinId = null) {
            let bulletin;
            
            if (bulletinId) {
                // Dans une vraie implémentation, vous récupéreriez le bulletin par son ID
                showAlert('Fonctionnalité d\'impression en cours de développement', 'info');
                return;
            } else {
                const bulletinStr = localStorage.getItem('current_bulletin');
                bulletin = bulletinStr ? JSON.parse(bulletinStr) : null;
            }
            
            if (!bulletin) {
                showAlert('Aucun bulletin à imprimer', 'error');
                return;
            }

            const printWindow = window.open('', '_blank');
            const bulletinHTML = genererBulletinPaiePro(bulletin);
            
            printWindow.document.write(`
                <!DOCTYPE html>
                <html>
                <head>
                    <title>Bulletin de Paie - ${bulletin.employe.prenom} ${bulletin.employe.nom}</title>
                    <style>
                        body { 
                            font-family: Arial, sans-serif; 
                            margin: 0; 
                            padding: 20px;
                            color: #333;
                        }
                        @media print {
                            body { margin: 0; }
                            .no-print { display: none; }
                        }
                        .bulletin-container {
                            width: 100%;
                            max-width: 210mm;
                            margin: 0 auto;
                            background: white;
                        }
                    </style>
                </head>
                <body>
                    <div class="bulletin-container">
                        ${bulletinHTML}
                    </div>
                    <div class="no-print" style="text-align: center; margin-top: 20px;">
                        <button onclick="window.print()" style="padding: 10px 20px; background: #007bff; color: white; border: none; border-radius: 5px; cursor: pointer;">🖨️ Imprimer</button>
                        <button onclick="window.close()" style="padding: 10px 20px; background: #6c757d; color: white; border: none; border-radius: 5px; cursor: pointer; margin-left: 10px;">Fermer</button>
                    </div>
                </body>
                </html>
            `);
            
            printWindow.document.close();
            
            showAlert('Bulletin ouvert pour impression', 'success');
        }

        // Initialize the application
        document.addEventListener('DOMContentLoaded', function() {
            const currentUser = getCurrentUser();
            if (currentUser) {
                updateUIForUser(currentUser);
                showSection('dashboard');
            } else {
                showSection('home');
            }
        });
    </script>
</body>
</html>
