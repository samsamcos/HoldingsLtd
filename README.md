<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Samsamco Empire — Command Centre</title>
    <link href="https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800;900&family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
        :root {
            --bg: #06080f;
            --bg-raised: #0d1117;
            --bg-card: #131820;
            --bg-input: #0a0e16;
            --border: #1e2736;
            --border-bright: #2a3548;
            --text: #e2e8f0;
            --text-dim: #64748b;
            --text-faint: #3e4a5c;
            --accent: #3b82f6;
            --accent-glow: rgba(59, 130, 246, 0.15);
            --engine: #ef4444;
            --engine-glow: rgba(239, 68, 68, 0.1);
            --green: #10b981;
            --purple: #8b5cf6;
            --amber: #f59e0b;
            --cyan: #06b6d4;
            --pink: #ec4899;
        }

        * { margin: 0; padding: 0; box-sizing: border-box; }

        body {
            font-family: 'Outfit', sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
        }

        /* ═══════ UTILITY ═══════ */
        .mono { font-family: 'JetBrains Mono', monospace; }
        .dim { color: var(--text-dim); }
        .faint { color: var(--text-faint); }
        .accent { color: var(--accent); }
        .green { color: var(--green); }
        .engine-color { color: var(--engine); }
        .small { font-size: 0.78rem; }
        .tag {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 4px;
            font-size: 0.7rem;
            font-weight: 600;
            letter-spacing: 0.5px;
            text-transform: uppercase;
        }
        .tag-engine { background: rgba(239,68,68,0.15); color: #fca5a5; border: 1px solid rgba(239,68,68,0.3); }
        .tag-sub { background: rgba(59,130,246,0.12); color: #93c5fd; border: 1px solid rgba(59,130,246,0.25); }
        .tag-active { background: rgba(16,185,129,0.12); color: #6ee7b7; border: 1px solid rgba(16,185,129,0.25); }

        /* ═══════ TOPBAR ═══════ */
        .topbar {
            background: var(--bg-raised);
            border-bottom: 1px solid var(--border);
            padding: 16px 28px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            z-index: 50;
            backdrop-filter: blur(12px);
        }
        .topbar-brand {
            display: flex;
            align-items: center;
            gap: 14px;
            cursor: pointer;
        }
        .topbar-logo {
            width: 38px; height: 38px;
            background: linear-gradient(135deg, var(--engine), #b91c1c);
            border-radius: 8px;
            display: flex; align-items: center; justify-content: center;
            font-weight: 900; font-size: 1.1rem;
            box-shadow: 0 0 20px rgba(239,68,68,0.2);
        }
        .topbar-title { font-weight: 700; font-size: 1.15rem; letter-spacing: -0.02em; }
        .topbar-sub { font-size: 0.75rem; color: var(--text-dim); margin-top: 1px; }
        .topbar-actions { display: flex; gap: 8px; }

        /* ═══════ BREADCRUMB ═══════ */
        .breadcrumb {
            padding: 12px 28px;
            font-size: 0.82rem;
            color: var(--text-dim);
            border-bottom: 1px solid var(--border);
            background: var(--bg);
            display: flex;
            align-items: center;
            gap: 6px;
        }
        .breadcrumb a {
            color: var(--accent);
            text-decoration: none;
            cursor: pointer;
        }
        .breadcrumb a:hover { text-decoration: underline; }
        .breadcrumb .sep { color: var(--text-faint); }

        /* ═══════ MAIN CONTENT ═══════ */
        .content { padding: 28px; max-width: 1400px; margin: 0 auto; }

        /* ═══════ ENGINE ROOM HERO ═══════ */
        .engine-hero {
            position: relative;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 28px 32px;
            margin-bottom: 32px;
            overflow: hidden;
        }
        .engine-hero::before {
            content: '';
            position: absolute;
            top: 0; left: 0; right: 0;
            height: 3px;
            background: linear-gradient(90deg, var(--engine), #f97316, var(--engine));
        }
        .engine-hero::after {
            content: '';
            position: absolute;
            top: 0; right: 0;
            width: 300px; height: 100%;
            background: radial-gradient(ellipse at top right, rgba(239,68,68,0.06), transparent 70%);
            pointer-events: none;
        }
        .engine-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1fr;
            gap: 20px;
            margin-top: 18px;
        }
        .engine-stat {
            background: rgba(255,255,255,0.02);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 14px;
        }
        .engine-stat-label { font-size: 0.72rem; text-transform: uppercase; letter-spacing: 0.8px; color: var(--text-faint); margin-bottom: 6px; }
        .engine-stat-value { font-size: 1.4rem; font-weight: 700; }

        /* ═══════ COMPANY GRID ═══════ */
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
        }
        .section-title { font-size: 1.2rem; font-weight: 700; }
        .section-count { font-size: 0.8rem; color: var(--text-dim); }

        .company-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(340px, 1fr));
            gap: 16px;
            margin-bottom: 40px;
        }

        .company-card {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.2s;
            position: relative;
            overflow: hidden;
        }
        .company-card:hover {
            border-color: var(--border-bright);
            transform: translateY(-2px);
            box-shadow: 0 8px 24px rgba(0,0,0,0.3);
        }
        .company-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0; right: 0;
            height: 3px;
        }
        .company-card-head {
            display: flex;
            justify-content: space-between;
            align-items: flex-start;
            margin-bottom: 12px;
        }
        .company-card-name { font-weight: 700; font-size: 1rem; }
        .company-card-type { font-size: 0.75rem; color: var(--text-dim); margin-top: 2px; }
        .company-card-desc {
            font-size: 0.82rem;
            color: var(--text-dim);
            line-height: 1.5;
            margin-bottom: 14px;
            min-height: 40px;
        }
        .company-card-stats {
            display: flex;
            gap: 16px;
            padding-top: 12px;
            border-top: 1px solid var(--border);
            font-size: 0.78rem;
        }
        .company-card-stat { display: flex; flex-direction: column; gap: 2px; }
        .company-card-stat-label { color: var(--text-faint); font-size: 0.68rem; text-transform: uppercase; letter-spacing: 0.5px; }
        .company-card-stat-val { font-weight: 600; }
        .company-card-actions {
            position: absolute;
            top: 14px; right: 14px;
            display: flex; gap: 4px;
            opacity: 0;
            transition: opacity 0.15s;
        }
        .company-card:hover .company-card-actions { opacity: 1; }

        .add-company-card {
            background: transparent;
            border: 2px dashed var(--border);
            border-radius: 12px;
            padding: 20px;
            cursor: pointer;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 180px;
            transition: all 0.2s;
            color: var(--text-faint);
        }
        .add-company-card:hover {
            border-color: var(--accent);
            color: var(--accent);
            background: var(--accent-glow);
        }
        .add-company-card .plus { font-size: 2rem; font-weight: 300; margin-bottom: 6px; }

        /* ═══════ SUB-PAGE: COMPANY DETAIL ═══════ */
        .detail-hero {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 14px;
            padding: 28px 32px;
            margin-bottom: 24px;
            position: relative;
            overflow: hidden;
        }
        .detail-hero::before {
            content: '';
            position: absolute;
            top: 0; left: 0; right: 0;
            height: 3px;
        }
        .detail-title { font-size: 1.5rem; font-weight: 800; }
        .detail-meta {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 16px;
            margin-top: 20px;
        }
        .detail-field {
            background: rgba(255,255,255,0.02);
            border: 1px solid var(--border);
            border-radius: 8px;
            padding: 12px;
        }
        .detail-field-label { font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.6px; color: var(--text-faint); margin-bottom: 4px; }
        .detail-field-val { font-size: 0.92rem; font-weight: 500; }

        /* HOST / GROUP SECTION IN DETAIL */
        .group-section { margin-bottom: 28px; }
        .group-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 12px 16px;
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 10px 10px 0 0;
        }
        .group-title { font-weight: 700; font-size: 0.95rem; }
        .group-count { font-size: 0.78rem; color: var(--text-dim); }
        .group-body {
            background: var(--bg-raised);
            border: 1px solid var(--border);
            border-top: none;
            border-radius: 0 0 10px 10px;
            max-height: 400px;
            overflow-y: auto;
        }
        .group-body::-webkit-scrollbar { width: 5px; }
        .group-body::-webkit-scrollbar-track { background: var(--bg); }
        .group-body::-webkit-scrollbar-thumb { background: var(--border); border-radius: 3px; }

        .host-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px 16px;
            border-bottom: 1px solid var(--border);
            font-size: 0.84rem;
            transition: background 0.1s;
        }
        .host-row:last-child { border-bottom: none; }
        .host-row:hover { background: rgba(255,255,255,0.02); }
        .host-name { font-weight: 600; }
        .host-detail { color: var(--text-dim); font-size: 0.76rem; margin-top: 2px; }
        .host-actions { display: flex; gap: 4px; }

        .empty-group {
            padding: 30px;
            text-align: center;
            color: var(--text-faint);
            font-size: 0.85rem;
        }

        /* ═══════ BUTTONS ═══════ */
        .btn {
            display: inline-flex;
            align-items: center;
            gap: 6px;
            padding: 8px 16px;
            border-radius: 6px;
            border: none;
            font-family: 'Outfit', sans-serif;
            font-weight: 600;
            font-size: 0.82rem;
            cursor: pointer;
            transition: all 0.15s;
        }
        .btn-primary { background: var(--accent); color: white; }
        .btn-primary:hover { background: #2563eb; }
        .btn-ghost { background: transparent; color: var(--text-dim); border: 1px solid var(--border); }
        .btn-ghost:hover { background: rgba(255,255,255,0.04); color: var(--text); border-color: var(--border-bright); }
        .btn-danger { background: rgba(239,68,68,0.15); color: #fca5a5; border: 1px solid rgba(239,68,68,0.3); }
        .btn-danger:hover { background: rgba(239,68,68,0.25); }
        .btn-sm { padding: 4px 10px; font-size: 0.75rem; }
        .btn-generate {
            width: 100%;
            padding: 10px;
            background: transparent;
            border: 1px dashed var(--border);
            color: var(--text-faint);
            font-family: 'Outfit', sans-serif;
            font-size: 0.82rem;
            border-radius: 8px;
            cursor: pointer;
            transition: all 0.15s;
            margin-top: 8px;
        }
        .btn-generate:hover { border-color: var(--accent); color: var(--accent); }

        /* ═══════ MODAL ═══════ */
        .modal-overlay {
            position: fixed;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: rgba(0,0,0,0.75);
            backdrop-filter: blur(6px);
            display: none;
            justify-content: center;
            align-items: flex-start;
            padding-top: 80px;
            z-index: 100;
            overflow-y: auto;
        }
        .modal-overlay.open { display: flex; }
        .modal {
            background: var(--bg-card);
            border: 1px solid var(--border-bright);
            border-radius: 14px;
            padding: 28px;
            width: 90%;
            max-width: 560px;
            box-shadow: 0 20px 60px rgba(0,0,0,0.5);
            margin-bottom: 40px;
        }
        .modal-title { font-size: 1.15rem; font-weight: 700; margin-bottom: 20px; }
        .form-row { margin-bottom: 16px; }
        .form-label {
            display: block;
            font-size: 0.75rem;
            font-weight: 600;
            text-transform: uppercase;
            letter-spacing: 0.6px;
            color: var(--text-dim);
            margin-bottom: 6px;
        }
        .form-input, .form-select, .form-textarea {
            width: 100%;
            padding: 10px 14px;
            background: var(--bg-input);
            border: 1px solid var(--border);
            color: var(--text);
            border-radius: 7px;
            font-family: 'Outfit', sans-serif;
            font-size: 0.88rem;
            transition: border-color 0.15s;
        }
        .form-input:focus, .form-select:focus, .form-textarea:focus {
            outline: none;
            border-color: var(--accent);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }
        .form-textarea { resize: vertical; min-height: 80px; }
        .form-hint { font-size: 0.72rem; color: var(--text-faint); margin-top: 4px; }
        .form-actions { display: flex; justify-content: flex-end; gap: 8px; margin-top: 24px; }

        .form-grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        /* ═══════ NOTES SECTION ═══════ */
        .notes-section {
            background: var(--bg-card);
            border: 1px solid var(--border);
            border-radius: 12px;
            padding: 20px;
            margin-top: 24px;
        }
        .notes-area {
            width: 100%;
            min-height: 120px;
            background: var(--bg-input);
            border: 1px solid var(--border);
            border-radius: 8px;
            color: var(--text);
            font-family: 'JetBrains Mono', monospace;
            font-size: 0.82rem;
            padding: 14px;
            resize: vertical;
            margin-top: 10px;
        }
        .notes-area:focus { outline: none; border-color: var(--accent); }
        .notes-area:disabled { opacity: 0.6; cursor: not-allowed; }

        /* ═══════ RESPONSIVE ═══════ */
        @media (max-width: 768px) {
            .content { padding: 16px; }
            .engine-grid { grid-template-columns: 1fr; }
            .company-grid { grid-template-columns: 1fr; }
            .detail-meta { grid-template-columns: 1fr; }
            .form-grid-2 { grid-template-columns: 1fr; }
            .topbar { padding: 12px 16px; }
        }

        /* ═══════ ANIMATIONS ═══════ */
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(8px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .animate-in { animation: fadeIn 0.3s ease-out; }

        /* color helper for company cards */
        .color-blue::before { background: var(--accent); }
        .color-green::before { background: var(--green); }
        .color-purple::before { background: var(--purple); }
        .color-amber::before { background: var(--amber); }
        .color-cyan::before { background: var(--cyan); }
        .color-pink::before { background: var(--pink); }
        .color-red::before { background: var(--engine); }

        /* Group color headers */
        .gh-blue { border-left: 3px solid var(--accent); }
        .gh-green { border-left: 3px solid var(--green); }
        .gh-purple { border-left: 3px solid var(--purple); }
        .gh-amber { border-left: 3px solid var(--amber); }
        .gh-cyan { border-left: 3px solid var(--cyan); }
        .gh-pink { border-left: 3px solid var(--pink); }

        /* EXPORT BAR */
        .export-bar {
            display: flex;
            gap: 8px;
            margin-top: 32px;
            padding-top: 20px;
            border-top: 1px solid var(--border);
            flex-wrap: wrap;
        }
    </style>
</head>
<body>

<div class="topbar">
    <div class="topbar-brand" onclick="navigateHome()">
        <div class="topbar-logo">S</div>
        <div>
            <div class="topbar-title">SAMSAMCO HOLDINGS</div>
            <div class="topbar-sub">Command Centre — Multi-Entity Empire</div>
        </div>
    </div>
    <div class="topbar-actions" id="topbar-controls">
        </div>
</div>

<div class="breadcrumb" id="breadcrumb">
    <a onclick="navigateHome()">Empire</a>
</div>

<div class="content" id="app"></div>

<div class="modal-overlay" id="modal">
    <div class="modal" id="modal-body"></div>
</div>

<script>
// ╔══════════════════════════════════════════════════════════╗
// ║  AUTHENTICATION STATE                                   ║
// ╚══════════════════════════════════════════════════════════╝

// Change your master credentials here
const ADMIN_USER = "admin";
const ADMIN_PASS = "Samsamco2026"; 

let isLoggedIn = false;

function openLoginModal() {
    openModal(`
        <div class="modal-title">Authentication Required</div>
        <div class="form-row">
            <label class="form-label">Username</label>
            <input type="text" class="form-input" id="auth-user" autocomplete="off">
        </div>
        <div class="form-row">
            <label class="form-label">Password</label>
            <input type="password" class="form-input" id="auth-pass" autocomplete="off">
        </div>
        <div id="auth-error" style="color:var(--engine); font-size:0.8rem; margin-top:10px; display:none;">
            Invalid credentials. Access denied.
        </div>
        <div class="form-actions">
            <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
            <button class="btn btn-primary" onclick="doLogin()">Unlock Controls</button>
        </div>
    `);
}

function doLogin() {
    const u = document.getElementById('auth-user').value;
    const p = document.getElementById('auth-pass').value;
    if (u === ADMIN_USER && p === ADMIN_PASS) {
        isLoggedIn = true;
        closeModal();
        render();
    } else {
        document.getElementById('auth-error').style.display = 'block';
    }
}

function doLogout() {
    isLoggedIn = false;
    render();
}

function renderTopbarControls() {
    const container = document.getElementById('topbar-controls');
    container.innerHTML = `
        <button class="btn btn-ghost btn-sm" onclick="exportAllData()">⬇ Export Data</button>
        ${isLoggedIn ? `
        <label class="btn btn-ghost btn-sm" style="cursor:pointer;">
            ⬆ Import Data
            <input type="file" accept=".json" onchange="importData(event)" style="display:none;">
        </label>
        <button class="btn btn-danger btn-sm" onclick="doLogout()">🔒 Lock Empire</button>
        ` : `
        <button class="btn btn-primary btn-sm" onclick="openLoginModal()">🔑 Admin Login</button>
        `}
    `;
}

// ╔══════════════════════════════════════════════════════════╗
// ║  SAMSAMCO EMPIRE — DATA LAYER                           ║
// ╚══════════════════════════════════════════════════════════╝

const STORAGE_KEY = "samsamcoEmpireV3";
const COLORS = ["blue","green","purple","amber","cyan","pink"];

function getDefaultData() {
    return {
        engine: {
            name: "Samsamco Holdings Ltd",
            role: "Engine Room & Treasury",
            companyNumber: "Company 16",
            assets: "82 VMs, Unraid/Proxmox Rack, Economy 7 Power",
            investmentVault: "S&P 500 Index — Long-term Wealth",
            personalDraw: "Monthly Dividend to Personal Account",
            notes: "All subsidiary companies pay processing fees back to Holdings. Holdings manages all infrastructure, VMs, API keys, and central tech stack. Family members can be added as shareholders in specific subsidiaries without touching the parent holding company."
        },
        companies: [
            {
                id: "media",
                name: "Samsamco Media Ltd",
                type: "Content & YouTube Automation",
                color: "purple",
                description: "128-host architecture across 4 groups. Pro channels use HeyGen/OmniHuman AI presenters. Commercial channels run FFmpeg shorts automation at scale.",
                registered: "2026",
                bankAccount: "Revolut Business — Media",
                stripe: "Stripe Org — Media Payments",
                domain: "samsamco-media.com",
                revolut: "Revolut Media Master Card",
                notes: "Each host is a VM running dedicated channel automation. 8-week production cycles. Revenue from YouTube AdSense + affiliate links in descriptions.",
                groups: [
                    {
                        id: "pro",
                        name: "Pro Account",
                        color: "purple",
                        target: "192 Pro Channels",
                        description: "HeyGen / OmniHuman Active SIM — AI presenter-led content",
                        hosts: []
                    },
                    {
                        id: "dropshipping",
                        name: "Dropshipping Account",
                        color: "green",
                        target: "180 Commercial Channels",
                        description: "Product review & unboxing content driving Shopify store traffic",
                        hosts: []
                    },
                    {
                        id: "extra",
                        name: "Extra Account",
                        color: "amber",
                        target: "180 Commercial Channels",
                        description: "Niche content — compilations, tutorials, listicles",
                        hosts: []
                    },
                    {
                        id: "affiliate",
                        name: "Affiliate Account",
                        color: "cyan",
                        target: "180 Commercial Channels",
                        description: "Amazon affiliate & CPA offer content funnels",
                        hosts: []
                    }
                ]
            },
            {
                id: "dropshipping",
                name: "Samsamco Dropshipping Ltd",
                type: "E-Commerce & Shopify Stores",
                color: "green",
                description: "Multi-store Shopify/WooCommerce operation. VPS-based store management with virtual cards for ad spend isolation.",
                registered: "2026",
                bankAccount: "Revolut Business — Dropshipping",
                stripe: "Stripe Org — Drop Payments",
                domain: "samsamco-drop.com",
                revolut: "Revolut Drop Master Card",
                notes: "USA and EU store variants. Each store has isolated ad spend via Revolut virtual cards. Facebook Ads + TikTok Ads funnels.",
                groups: [
                    {
                        id: "usa-stores",
                        name: "USA Stores",
                        color: "blue",
                        target: "US Market Shopify Stores",
                        description: "US-targeted stores with US VPS addresses and payment processing",
                        hosts: []
                    },
                    {
                        id: "eu-stores",
                        name: "EU Stores",
                        color: "green",
                        target: "EU Market Shopify Stores",
                        description: "EU-targeted stores with European payment gateways",
                        hosts: []
                    },
                    {
                        id: "uk-stores",
                        name: "UK Stores",
                        color: "amber",
                        target: "UK Market Stores",
                        description: "UK domestic stores — no customs complications",
                        hosts: []
                    }
                ]
            },
            {
                id: "passive",
                name: "Samsamco Passive Ltd",
                type: "Passive Income Streams",
                color: "amber",
                description: "Set-and-forget income: KDP publishing, print-on-demand, niche websites, and digital product sales.",
                registered: "2026",
                bankAccount: "Revolut Business — Passive",
                stripe: "Stripe Org — Passive Income",
                domain: "samsamco-passive.com",
                revolut: "Revolut Passive Master Card",
                notes: "85 passive income sites. Revenue from ads, affiliate links, and direct digital product sales. Minimal maintenance once set up.",
                groups: [
                    {
                        id: "kdp",
                        name: "KDP Publishing",
                        color: "amber",
                        target: "Amazon KDP Books & Journals",
                        description: "Low-content books, journals, planners on Amazon",
                        hosts: []
                    },
                    {
                        id: "pod",
                        name: "Print on Demand",
                        color: "pink",
                        target: "Spreadshirt / Redbubble / Merch",
                        description: "T-shirts, mugs, phone cases — automated design uploads",
                        hosts: []
                    },
                    {
                        id: "sites",
                        name: "Niche Websites",
                        color: "cyan",
                        target: "85 Passive Income Sites",
                        description: "SEO content sites with display ads and affiliate links",
                        hosts: []
                    }
                ]
            }
        ]
    };
}

let empire = loadData();

function loadData() {
    try {
        const raw = localStorage.getItem(STORAGE_KEY);
        if (raw) return JSON.parse(raw);
    } catch(e) {}
    return getDefaultData();
}

function saveData() {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(empire));
}

// ╔══════════════════════════════════════════════════════════╗
// ║  NAVIGATION STATE                                       ║
// ╚══════════════════════════════════════════════════════════╝

let currentView = "home"; 
let currentCompanyId = null;

function navigateHome() {
    currentView = "home";
    currentCompanyId = null;
    render();
}

function navigateToCompany(companyId) {
    currentView = "company";
    currentCompanyId = companyId;
    render();
}

// ╔══════════════════════════════════════════════════════════╗
// ║  RENDER ENGINE                                          ║
// ╚══════════════════════════════════════════════════════════╝

function render() {
    renderTopbarControls();
    const app = document.getElementById('app');
    const bc = document.getElementById('breadcrumb');

    if (currentView === "home") {
        bc.innerHTML = `<a onclick="navigateHome()">Empire</a>`;
        app.innerHTML = renderHome();
    } else if (currentView === "company") {
        const co = empire.companies.find(c => c.id === currentCompanyId);
        bc.innerHTML = `<a onclick="navigateHome()">Empire</a> <span class="sep">›</span> <span>${co.name}</span>`;
        app.innerHTML = renderCompanyDetail(co);
    }

    app.classList.remove('animate-in');
    void app.offsetWidth;
    app.classList.add('animate-in');
}

// ═══════ HOME VIEW ═══════
function renderHome() {
    const e = empire.engine;
    const totalHosts = empire.companies.reduce((sum, co) => {
        return sum + co.groups.reduce((gs, g) => gs + g.hosts.length, 0);
    }, 0);
    const totalGroups = empire.companies.reduce((sum, co) => sum + co.groups.length, 0);

    let html = `
        <div class="engine-hero">
            <div style="display:flex; justify-content:space-between; align-items:flex-start; flex-wrap:wrap; gap:12px;">
                <div>
                    <span class="tag tag-engine">ENGINE ROOM</span>
                    <h2 style="font-size:1.35rem; font-weight:800; margin-top:8px;">${e.name}</h2>
                    <div class="dim" style="margin-top:4px; font-size:0.88rem;">${e.role} — ${e.companyNumber}</div>
                </div>
                ${isLoggedIn ? `<button class="btn btn-ghost btn-sm" onclick="editEngine()">✎ Edit Holdings</button>` : ''}
            </div>
            <div class="engine-grid">
                <div class="engine-stat">
                    <div class="engine-stat-label">Infrastructure</div>
                    <div class="engine-stat-value">${e.assets.split(',')[0]}</div>
                    <div class="small dim" style="margin-top:4px;">${e.assets}</div>
                </div>
                <div class="engine-stat">
                    <div class="engine-stat-label">Investment Vault</div>
                    <div class="engine-stat-value green">S&P 500</div>
                    <div class="small dim" style="margin-top:4px;">${e.investmentVault}</div>
                </div>
                <div class="engine-stat">
                    <div class="engine-stat-label">Empire Scale</div>
                    <div class="engine-stat-value accent">${empire.companies.length} Companies</div>
                    <div class="small dim" style="margin-top:4px;">${totalGroups} groups · ${totalHosts} active hosts/items</div>
                </div>
            </div>
            ${e.notes ? `<div style="margin-top:16px; padding:12px; background:rgba(255,255,255,0.02); border:1px solid var(--border); border-radius:8px; font-size:0.82rem; color:var(--text-dim); line-height:1.6;">${e.notes}</div>` : ''}
        </div>

        <div class="section-header">
            <div>
                <div class="section-title">Subsidiary Companies</div>
                <div class="section-count">${empire.companies.length} active entities — all paying fees to Engine Room</div>
            </div>
        </div>
        <div class="company-grid">
    `;

    empire.companies.forEach(co => {
        const hostCount = co.groups.reduce((s, g) => s + g.hosts.length, 0);
        html += `
            <div class="company-card color-${co.color}" onclick="navigateToCompany('${co.id}')">
                ${isLoggedIn ? `
                <div class="company-card-actions">
                    <button class="btn btn-ghost btn-sm" onclick="event.stopPropagation(); editCompany('${co.id}')">✎</button>
                    <button class="btn btn-danger btn-sm" onclick="event.stopPropagation(); deleteCompany('${co.id}')">✕</button>
                </div>
                ` : ''}
                <div class="company-card-head">
                    <div>
                        <div class="company-card-name">${co.name}</div>
                        <div class="company-card-type">${co.type}</div>
                    </div>
                    <span class="tag tag-sub">${co.color.toUpperCase()}</span>
                </div>
                <div class="company-card-desc">${co.description || 'No description set.'}</div>
                <div class="company-card-stats">
                    <div class="company-card-stat">
                        <div class="company-card-stat-label">Groups</div>
                        <div class="company-card-stat-val">${co.groups.length}</div>
                    </div>
                    <div class="company-card-stat">
                        <div class="company-card-stat-label">Active Items</div>
                        <div class="company-card-stat-val">${hostCount}</div>
                    </div>
                    <div class="company-card-stat">
                        <div class="company-card-stat-label">Bank</div>
                        <div class="company-card-stat-val" style="font-size:0.72rem;">${co.bankAccount || '—'}</div>
                    </div>
                    <div class="company-card-stat">
                        <div class="company-card-stat-label">Domain</div>
                        <div class="company-card-stat-val" style="font-size:0.72rem;">${co.domain || '—'}</div>
                    </div>
                </div>
            </div>
        `;
    });

    if (isLoggedIn) {
        html += `
            <div class="add-company-card" onclick="addCompany()">
                <div class="plus">+</div>
                <div style="font-size:0.88rem; font-weight:600;">Add Subsidiary Company</div>
                <div style="font-size:0.75rem; margin-top:4px;">Samsamco [Something] Ltd</div>
            </div>
        `;
    }

    html += `
        </div>
        ${isLoggedIn ? `
        <div class="export-bar" style="justify-content:flex-end;">
            <button class="btn btn-danger btn-sm" onclick="resetAll()">⚠ Hard Reset to Default Empire</button>
        </div>
        ` : ''}
    `;

    return html;
}

// ═══════ COMPANY DETAIL VIEW ═══════
function renderCompanyDetail(co) {
    let html = `
        <div class="detail-hero color-${co.color}">
            <div style="display:flex; justify-content:space-between; align-items:flex-start; flex-wrap:wrap; gap:12px;">
                <div>
                    <span class="tag tag-active">ACTIVE SUBSIDIARY</span>
                    <div class="detail-title" style="margin-top:8px;">${co.name}</div>
                    <div class="dim" style="margin-top:4px;">${co.type}</div>
                </div>
                ${isLoggedIn ? `
                <div style="display:flex; gap:8px;">
                    <button class="btn btn-ghost btn-sm" onclick="editCompany('${co.id}')">✎ Edit Company</button>
                    <button class="btn btn-primary btn-sm" onclick="addGroup('${co.id}')">+ Add Group</button>
                </div>
                ` : ''}
            </div>
            <div class="detail-meta">
                <div class="detail-field">
                    <div class="detail-field-label">Description</div>
                    <div class="detail-field-val" style="font-size:0.82rem; color:var(--text-dim); line-height:1.5;">${co.description || '—'}</div>
                </div>
                <div class="detail-field">
                    <div class="detail-field-label">Bank Account</div>
                    <div class="detail-field-val">${co.bankAccount || '—'}</div>
                </div>
                <div class="detail-field">
                    <div class="detail-field-label">Stripe / Payments</div>
                    <div class="detail-field-val">${co.stripe || '—'}</div>
                </div>
                <div class="detail-field">
                    <div class="detail-field-label">Domain (5-Year Rule)</div>
                    <div class="detail-field-val mono">${co.domain || '—'}</div>
                </div>
                <div class="detail-field">
                    <div class="detail-field-label">Revolut Card</div>
                    <div class="detail-field-val">${co.revolut || '—'}</div>
                </div>
                <div class="detail-field">
                    <div class="detail-field-label">Registered</div>
                    <div class="detail-field-val">${co.registered || '—'}</div>
                </div>
            </div>
        </div>
    `;

    // GROUPS
    co.groups.forEach(group => {
        const hostCount = group.hosts.length;
        html += `
            <div class="group-section">
                <div class="group-header gh-${group.color}">
                    <div>
                        <div class="group-title">${group.name}</div>
                        <div class="small dim">${group.description || ''} — Target: ${group.target || 'N/A'}</div>
                    </div>
                    <div style="display:flex; align-items:center; gap:10px;">
                        <span class="group-count">${hostCount} items</span>
                        ${isLoggedIn ? `
                        <button class="btn btn-ghost btn-sm" onclick="editGroup('${co.id}','${group.id}')">✎</button>
                        <button class="btn btn-danger btn-sm" onclick="deleteGroup('${co.id}','${group.id}')">✕</button>
                        <button class="btn btn-primary btn-sm" onclick="addHost('${co.id}','${group.id}')">+ Add</button>
                        ` : ''}
                    </div>
                </div>
                <div class="group-body">
        `;

        if (hostCount === 0) {
            html += `<div class="empty-group">No items deployed in this group yet.</div>`;
        } else {
            group.hosts.forEach(h => {
                html += `
                    <div class="host-row">
                        <div>
                            <div class="host-name">${h.name}</div>
                            <div class="host-detail">💳 ${h.card || '—'} · ⚙️ ${h.logic || '—'}</div>
                            ${h.notes ? `<div class="host-detail">📝 ${h.notes}</div>` : ''}
                        </div>
                        ${isLoggedIn ? `
                        <div class="host-actions">
                            <button class="btn btn-ghost btn-sm" onclick="editHost('${co.id}','${group.id}',${h.id})">✎</button>
                            <button class="btn btn-danger btn-sm" onclick="deleteHost('${co.id}','${group.id}',${h.id})">✕</button>
                        </div>
                        ` : ''}
                    </div>
                `;
            });
        }

        html += `
                </div>
                ${isLoggedIn ? `
                <button class="btn-generate" onclick="bulkGenerate('${co.id}','${group.id}')">⚡ Auto-Generate 32 Hosts for ${group.name}</button>
                ` : ''}
            </div>
        `;
    });

    // NOTES
    html += `
        <div class="notes-section">
            <div style="display:flex; justify-content:space-between; align-items:center;">
                <h3 style="font-size:0.95rem;">Company Notes & Strategy</h3>
                ${isLoggedIn ? `<button class="btn btn-ghost btn-sm" onclick="saveCompanyNotes('${co.id}')">💾 Save Notes</button>` : ''}
            </div>
            <textarea class="notes-area" id="company-notes-${co.id}" placeholder="Write notes, strategy, reminders..." ${isLoggedIn ? '' : 'disabled'}>${co.notes || ''}</textarea>
        </div>
    `;

    return html;
}

// ╔══════════════════════════════════════════════════════════╗
// ║  MODAL FORMS (Protected Logic)                          ║
// ╚══════════════════════════════════════════════════════════╝

function openModal(html) {
    document.getElementById('modal-body').innerHTML = html;
    document.getElementById('modal').classList.add('open');
}

function closeModal() {
    document.getElementById('modal').classList.remove('open');
}

document.getElementById('modal').addEventListener('click', function(e) {
    if (e.target === this) closeModal();
});

function editEngine() {
    if(!isLoggedIn) return;
    const e = empire.engine;
    openModal(`
        <div class="modal-title">Edit Samsamco Holdings (Engine Room)</div>
        <div class="form-row">
            <label class="form-label">Company Name</label>
            <input class="form-input" id="f-eng-name" value="${esc(e.name)}">
        </div>
        <div class="form-row">
            <label class="form-label">Role</label>
            <input class="form-input" id="f-eng-role" value="${esc(e.role)}">
        </div>
        <div class="form-grid-2">
            <div class="form-row">
                <label class="form-label">Company Number</label>
                <input class="form-input" id="f-eng-num" value="${esc(e.companyNumber)}">
            </div>
            <div class="form-row">
                <label class="form-label">Investment Vault</label>
                <input class="form-input" id="f-eng-invest" value="${esc(e.investmentVault)}">
            </div>
        </div>
        <div class="form-row">
            <label class="form-label">Assets & Infrastructure</label>
            <input class="form-input" id="f-eng-assets" value="${esc(e.assets)}">
        </div>
        <div class="form-row">
            <label class="form-label">Personal Draw Method</label>
            <input class="form-input" id="f-eng-draw" value="${esc(e.personalDraw)}">
        </div>
        <div class="form-row">
            <label class="form-label">Notes & Strategy</label>
            <textarea class="form-textarea" id="f-eng-notes">${esc(e.notes || '')}</textarea>
        </div>
        <div class="form-actions">
            <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
            <button class="btn btn-primary" onclick="saveEngine()">Save Holdings</button>
        </div>
    `);
}

function saveEngine() {
    empire.engine.name = gv('f-eng-name');
    empire.engine.role = gv('f-eng-role');
    empire.engine.companyNumber = gv('f-eng-num');
    empire.engine.investmentVault = gv('f-eng-invest');
    empire.engine.assets = gv('f-eng-assets');
    empire.engine.personalDraw = gv('f-eng-draw');
    empire.engine.notes = gv('f-eng-notes');
    saveData(); closeModal(); render();
}

function addCompany() { if(isLoggedIn) openCompanyForm(null); }
function editCompany(id) { if(isLoggedIn) openCompanyForm(empire.companies.find(c => c.id === id)); }

function openCompanyForm(co) {
    const isEdit = !!co;
    const title = isEdit ? `Edit ${co.name}` : "Add New Subsidiary";
    const colorOptions = COLORS.map(c =>
        `<option value="${c}" ${co && co.color === c ? 'selected' : ''}>${c.charAt(0).toUpperCase() + c.slice(1)}</option>`
    ).join('');

    openModal(`
        <div class="modal-title">${title}</div>
        <div class="form-row">
            <label class="form-label">Company Name</label>
            <input class="form-input" id="f-co-name" value="${esc(co?.name || 'Samsamco ')}">
            <div class="form-hint">Keep the Samsamco [X] Ltd naming convention</div>
        </div>
        <div class="form-grid-2">
            <div class="form-row">
                <label class="form-label">Company Type</label>
                <input class="form-input" id="f-co-type" value="${esc(co?.type || '')}" placeholder="e.g. E-Commerce">
            </div>
            <div class="form-row">
                <label class="form-label">Theme Color</label>
                <select class="form-select" id="f-co-color">${colorOptions}</select>
            </div>
        </div>
        <div class="form-row">
            <label class="form-label">Description</label>
            <textarea class="form-textarea" id="f-co-desc">${esc(co?.description || '')}</textarea>
        </div>
        <div class="form-grid-2">
            <div class="form-row">
                <label class="form-label">Bank Account</label>
                <input class="form-input" id="f-co-bank" value="${esc(co?.bankAccount || '')}">
            </div>
            <div class="form-row">
                <label class="form-label">Stripe / Payments</label>
                <input class="form-input" id="f-co-stripe" value="${esc(co?.stripe || '')}">
            </div>
        </div>
        <div class="form-grid-2">
            <div class="form-row">
                <label class="form-label">Domain</label>
                <input class="form-input" id="f-co-domain" value="${esc(co?.domain || '')}">
            </div>
            <div class="form-row">
                <label class="form-label">Revolut Virtual Card</label>
                <input class="form-input" id="f-co-revolut" value="${esc(co?.revolut || '')}">
            </div>
        </div>
        <div class="form-row">
            <label class="form-label">Year Registered</label>
            <input class="form-input" id="f-co-reg" value="${esc(co?.registered || '2026')}">
        </div>
        <div class="form-actions">
            <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
            <button class="btn btn-primary" onclick="saveCompany(${isEdit ? `'${co.id}'` : 'null'})">${isEdit ? 'Save Changes' : 'Create Company'}</button>
        </div>
    `);
}

function saveCompany(existingId) {
    const name = gv('f-co-name') || 'Samsamco Unnamed Ltd';
    const data = {
        name,
        type: gv('f-co-type'),
        color: gv('f-co-color'),
        description: gv('f-co-desc'),
        bankAccount: gv('f-co-bank'),
        stripe: gv('f-co-stripe'),
        domain: gv('f-co-domain'),
        revolut: gv('f-co-revolut'),
        registered: gv('f-co-reg'),
    };

    if (existingId) {
        Object.assign(empire.companies.find(c => c.id === existingId), data);
    } else {
        data.id = name.toLowerCase().replace(/[^a-z0-9]/g, '-').replace(/-+/g, '-').slice(0, 30) + '-' + Date.now();
        data.notes = '';
        data.groups = [];
        empire.companies.push(data);
    }
    saveData(); closeModal(); render();
}

function deleteCompany(id) {
    if (!isLoggedIn) return;
    const co = empire.companies.find(c => c.id === id);
    if (confirm(`Delete "${co.name}" and all its groups/hosts? This cannot be undone.`)) {
        empire.companies = empire.companies.filter(c => c.id !== id);
        saveData();
        if (currentCompanyId === id) navigateHome();
        else render();
    }
}

function addGroup(companyId) { if(isLoggedIn) openGroupForm(companyId, null); }
function editGroup(companyId, groupId) {
    if(!isLoggedIn) return;
    const co = empire.companies.find(c => c.id === companyId);
    openGroupForm(companyId, co.groups.find(g => g.id === groupId));
}

function openGroupForm(companyId, group) {
    const isEdit = !!group;
    const colorOptions = COLORS.map(c =>
        `<option value="${c}" ${group && group.color === c ? 'selected' : ''}>${c.charAt(0).toUpperCase() + c.slice(1)}</option>`
    ).join('');

    openModal(`
        <div class="modal-title">${isEdit ? 'Edit Group' : 'Add New Group'}</div>
        <div class="form-row">
            <label class="form-label">Group Name</label>
            <input class="form-input" id="f-grp-name" value="${esc(group?.name || '')}">
        </div>
        <div class="form-grid-2">
            <div class="form-row">
                <label class="form-label">Target</label>
                <input class="form-input" id="f-grp-target" value="${esc(group?.target || '')}">
            </div>
            <div class="form-row">
                <label class="form-label">Color</label>
                <select class="form-select" id="f-grp-color">${colorOptions}</select>
            </div>
        </div>
        <div class="form-row">
            <label class="form-label">Description</label>
            <textarea class="form-textarea" id="f-grp-desc">${esc(group?.description || '')}</textarea>
        </div>
        <div class="form-actions">
            <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
            <button class="btn btn-primary" onclick="saveGroup('${companyId}', ${isEdit ? `'${group.id}'` : 'null'})">${isEdit ? 'Save' : 'Create Group'}</button>
        </div>
    `);
}

function saveGroup(companyId, existingGroupId) {
    const co = empire.companies.find(c => c.id === companyId);
    const data = {
        name: gv('f-grp-name') || 'Unnamed Group',
        target: gv('f-grp-target'),
        color: gv('f-grp-color'),
        description: gv('f-grp-desc'),
    };

    if (existingGroupId) {
        Object.assign(co.groups.find(g => g.id === existingGroupId), data);
    } else {
        data.id = data.name.toLowerCase().replace(/[^a-z0-9]/g, '-').replace(/-+/g, '-') + '-' + Date.now();
        data.hosts = [];
        co.groups.push(data);
    }
    saveData(); closeModal(); render();
}

function deleteGroup(companyId, groupId) {
    if(!isLoggedIn) return;
    const co = empire.companies.find(c => c.id === companyId);
    if (confirm(`Delete this group and all its hosts?`)) {
        co.groups = co.groups.filter(g => g.id !== groupId);
        saveData(); render();
    }
}

function addHost(companyId, groupId) { if(isLoggedIn) openHostForm(companyId, groupId, null); }
function editHost(companyId, groupId, hostId) {
    if(!isLoggedIn) return;
    const co = empire.companies.find(c => c.id === companyId);
    const group = co.groups.find(g => g.id === groupId);
    openHostForm(companyId, groupId, group.hosts.find(h => h.id === hostId));
}

function openHostForm(companyId, groupId, host) {
    const isEdit = !!host;
    openModal(`
        <div class="modal-title">${isEdit ? 'Edit Item' : 'Add New Item'}</div>
        <div class="form-row">
            <label class="form-label">Name / VM ID</label>
            <input class="form-input" id="f-host-name" value="${esc(host?.name || '')}">
        </div>
        <div class="form-row">
            <label class="form-label">Virtual Card (Revolut)</label>
            <input class="form-input" id="f-host-card" value="${esc(host?.card || '')}">
        </div>
        <div class="form-row">
            <label class="form-label">Automation Logic</label>
            <input class="form-input" id="f-host-logic" value="${esc(host?.logic || '')}">
        </div>
        <div class="form-row">
            <label class="form-label">Domain / URL</label>
            <input class="form-input" id="f-host-domain" value="${esc(host?.domain || '')}">
        </div>
        <div class="form-row">
            <label class="form-label">Income Source</label>
            <input class="form-input" id="f-host-income" value="${esc(host?.income || '')}">
        </div>
        <div class="form-row">
            <label class="form-label">Notes</label>
            <textarea class="form-textarea" id="f-host-notes">${esc(host?.notes || '')}</textarea>
        </div>
        <div class="form-actions">
            <button class="btn btn-ghost" onclick="closeModal()">Cancel</button>
            <button class="btn btn-primary" onclick="saveHost('${companyId}','${groupId}',${isEdit ? host.id : 'null'})">${isEdit ? 'Save' : 'Add Item'}</button>
        </div>
    `);
}

function saveHost(companyId, groupId, existingId) {
    const co = empire.companies.find(c => c.id === companyId);
    const group = co.groups.find(g => g.id === groupId);
    const data = {
        name: gv('f-host-name') || 'Unnamed Host',
        card: gv('f-host-card'),
        logic: gv('f-host-logic'),
        domain: gv('f-host-domain'),
        income: gv('f-host-income'),
        notes: gv('f-host-notes'),
    };

    if (existingId) {
        Object.assign(group.hosts.find(h => h.id === existingId), data);
    } else {
        data.id = Date.now();
        group.hosts.push(data);
    }
    saveData(); closeModal(); render();
}

function deleteHost(companyId, groupId, hostId) {
    if(!isLoggedIn) return;
    const group = empire.companies.find(c => c.id === companyId).groups.find(g => g.id === groupId);
    group.hosts = group.hosts.filter(h => h.id !== hostId);
    saveData(); render();
}

function bulkGenerate(companyId, groupId) {
    if(!isLoggedIn) return;
    const group = empire.companies.find(c => c.id === companyId).groups.find(g => g.id === groupId);
    const count = prompt(`How many items to auto-generate for "${group.name}"?`, "32");
    if (!count || isNaN(count)) return;
    const n = parseInt(count);
    if (n < 1 || n > 200) { alert("Pick a number between 1 and 200."); return; }

    if (!confirm(`Generate ${n} items in "${group.name}"?`)) return;

    for (let i = 1; i <= n; i++) {
        const num = i.toString().padStart(2, '0');
        group.hosts.push({
            id: Date.now() + i,
            name: `${group.name} Host ${num}`,
            card: `${group.name} Card #${num}`,
            logic: group.description || 'Automation Worker',
            domain: '', income: '', notes: ''
        });
    }
    saveData(); render();
}

function saveCompanyNotes(companyId) {
    if(!isLoggedIn) return;
    const co = empire.companies.find(c => c.id === companyId);
    const el = document.getElementById(`company-notes-${companyId}`);
    if (el) {
        co.notes = el.value;
        saveData();
        const btn = el.previousElementSibling?.querySelector('button') || el.parentElement.querySelector('button');
        if (btn) {
            const orig = btn.textContent;
            btn.textContent = '✓ Saved!';
            setTimeout(() => btn.textContent = orig, 1500);
        }
    }
}

// ╔══════════════════════════════════════════════════════════╗
// ║  IMPORT / EXPORT / RESET                                ║
// ╚══════════════════════════════════════════════════════════╝

function exportAllData() {
    const blob = new Blob([JSON.stringify(empire, null, 2)], { type: 'application/json' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url;
    a.download = `samsamco-empire-backup-${new Date().toISOString().slice(0,10)}.json`;
    a.click();
    URL.revokeObjectURL(url);
}

function importData(event) {
    if(!isLoggedIn) return;
    const file = event.target.files[0];
    if (!file) return;
    const reader = new FileReader();
    reader.onload = function(e) {
        try {
            const data = JSON.parse(e.target.result);
            if (data.engine && data.companies) {
                if (confirm("Import this backup? This will replace all current data.")) {
                    empire = data;
                    saveData();
                    navigateHome();
                }
            } else { alert("Invalid backup file format."); }
        } catch(err) { alert("Error reading file: " + err.message); }
    };
    reader.readAsText(file);
    event.target.value = '';
}

function resetAll() {
    if(!isLoggedIn) return;
    if (confirm("⚠ FULL RESET: This wipes everything and restores the default 3-company empire. Are you absolutely sure?")) {
        empire = getDefaultData();
        saveData();
        navigateHome();
    }
}

function gv(id) { return document.getElementById(id)?.value?.trim() || ''; }
function esc(str) { return (str || '').replace(/"/g, '&quot;').replace(/</g, '&lt;').replace(/>/g, '&gt;'); }

// ═══════ BOOT ═══════
render();
</script>

</body>
</html>
