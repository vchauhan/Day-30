# Day-30
Supply Chain Optimizer
```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Supply Chain Builder</title>
<script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/@babel/standalone/babel.min.js"></script>
<style>
  :root{
    --bg:#0b0f1a;
    --bg-grad: radial-gradient(circle at 20% 0%, #142033 0%, #0b0f1a 55%);
    --card:#131a2a;
    --card-hover:#1b2438;
    --border:#232d43;
    --accent:#4f8cff;
    --accent2:#7c5cff;
    --green:#3ddc97;
    --yellow:#ffcc4d;
    --red:#ff5d6c;
    --text:#e9edf5;
    --text-dim:#93a0b8;
    --radius:18px;
  }
  *{box-sizing:border-box;}
  html,body{
    margin:0;padding:0;
    background:var(--bg-grad);
    color:var(--text);
    font-family:'Segoe UI', system-ui, -apple-system, Roboto, Helvetica, Arial, sans-serif;
    min-height:100vh;
  }
  #root{min-height:100vh;}
  .app-shell{
    max-width:1200px;
    margin:0 auto;
    padding:28px 20px 60px;
  }
  .topbar{
    display:flex;
    align-items:center;
    justify-content:space-between;
    margin-bottom:28px;
  }
  .brand{
    display:flex;align-items:center;gap:10px;
    font-weight:700;font-size:1.25rem;
    letter-spacing:0.3px;
  }
  .brand .dot{
    width:12px;height:12px;border-radius:50%;
    background:linear-gradient(135deg,var(--accent),var(--accent2));
    box-shadow:0 0 12px var(--accent);
  }
  .card{
    background:var(--card);
    border:1px solid var(--border);
    border-radius:var(--radius);
    padding:24px;
    transition:all 0.25s ease;
    animation:fadeIn 0.5s ease;
  }
  .card:hover{
    border-color:#31405f;
  }
  @keyframes fadeIn{
    from{opacity:0; transform:translateY(10px);}
    to{opacity:1; transform:translateY(0);}
  }
  .btn{
    background:linear-gradient(135deg,var(--accent),var(--accent2));
    color:#fff;
    border:none;
    padding:12px 22px;
    border-radius:12px;
    font-size:0.95rem;
    font-weight:600;
    cursor:pointer;
    transition:transform 0.15s ease, box-shadow 0.15s ease, opacity 0.15s ease;
    box-shadow:0 6px 18px rgba(79,140,255,0.25);
  }
  .btn:hover{
    transform:translateY(-2px);
    box-shadow:0 10px 24px rgba(79,140,255,0.35);
  }
  .btn:active{transform:translateY(0);}
  .btn.secondary{
    background:transparent;
    border:1px solid var(--border);
    box-shadow:none;
    color:var(--text);
  }
  .btn.secondary:hover{
    border-color:var(--accent);
    box-shadow:none;
  }
  .btn:disabled{
    opacity:0.5;
    cursor:not-allowed;
    transform:none;
  }
  .welcome-hero{
    text-align:center;
    padding:60px 20px;
  }
  .welcome-hero h1{
    font-size:2.6rem;
    margin-bottom:14px;
    background:linear-gradient(135deg,#fff,#9fb8ff);
    -webkit-background-clip:text;
    background-clip:text;
    color:transparent;
  }
  .welcome-hero p{
    color:var(--text-dim);
    font-size:1.1rem;
    max-width:640px;
    margin:0 auto 30px;
    line-height:1.6;
  }
  .info-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
    gap:16px;
    margin:36px 0;
    text-align:left;
  }
  .info-grid .card h3{margin:0 0 8px;font-size:1.05rem;}
  .info-grid .card p{margin:0;color:var(--text-dim);font-size:0.9rem;line-height:1.5;}
  .company-card{
    display:flex;
    gap:24px;
    align-items:center;
    flex-wrap:wrap;
  }
  .company-icon{
    font-size:3.4rem;
    width:90px;height:90px;
    display:flex;align-items:center;justify-content:center;
    background:linear-gradient(135deg,#1c2745,#111a30);
    border-radius:20px;
    border:1px solid var(--border);
  }
  .company-details h2{margin:0 0 6px;font-size:1.6rem;}
  .company-details .tag{
    display:inline-block;
    background:#1c2745;
    color:#a9c2ff;
    padding:3px 10px;
    border-radius:20px;
    font-size:0.78rem;
    margin-right:6px;
    margin-top:6px;
  }
  .layout{
    display:grid;
    grid-template-columns:1fr 300px;
    gap:24px;
    align-items:start;
  }
  @media (max-width:860px){
    .layout{grid-template-columns:1fr;}
    .metrics-panel{order:-1;}
  }
  .metrics-panel{
    position:sticky;
    top:20px;
    display:flex;
    flex-direction:column;
    gap:14px;
  }
  .metric-row{margin-bottom:14px;}
  .metric-row:last-child{margin-bottom:0;}
  .metric-label{
    display:flex;
    justify-content:space-between;
    font-size:0.85rem;
    margin-bottom:6px;
    color:var(--text-dim);
  }
  .metric-label span.value{color:var(--text);font-weight:600;}
  .bar-track{
    width:100%;
    height:10px;
    background:#0e1524;
    border-radius:6px;
    overflow:hidden;
    border:1px solid var(--border);
  }
  .bar-fill{
    height:100%;
    border-radius:6px;
    transition:width 0.7s cubic-bezier(.4,0,.2,1), background 0.4s ease;
  }
  .step-header{
    display:flex;
    justify-content:space-between;
    align-items:center;
    margin-bottom:6px;
  }
  .step-badge{
    font-size:0.75rem;
    color:var(--accent);
    text-transform:uppercase;
    letter-spacing:1px;
    font-weight:700;
  }
  .step-title{
    font-size:1.5rem;
    margin:4px 0 14px;
  }
  .concept-box{
    background:#0f1626;
    border:1px solid var(--border);
    border-radius:14px;
    padding:16px 18px;
    margin-bottom:22px;
  }
  .concept-box .row{
    margin-bottom:10px;
    line-height:1.55;
    font-size:0.92rem;
  }
  .concept-box .row:last-child{margin-bottom:0;}
  .concept-box b{color:#9fc0ff;}
  .options-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(230px,1fr));
    gap:16px;
  }
  .option-card{
    background:#101828;
    border:1px solid var(--border);
    border-radius:16px;
    padding:18px;
    cursor:pointer;
    transition:all 0.2s ease;
  }
  .option-card:hover{
    border-color:var(--accent);
    background:var(--card-hover);
    transform:translateY(-3px);
  }
  .option-card.selected{
    border-color:var(--green);
    box-shadow:0 0 0 1px var(--green);
  }
  .option-card h4{margin:0 0 8px;font-size:1.05rem;}
  .option-card p.short{
    color:var(--text-dim);
    font-size:0.85rem;
    margin:0;
    line-height:1.5;
  }
  .tradeoff-box{
    margin-top:20px;
    background:linear-gradient(135deg,#12203a,#0f1626);
    border:1px solid #2a3a5c;
    border-radius:14px;
    padding:18px;
    animation:fadeIn 0.4s ease;
  }
  .tradeoff-box .label{
    font-size:0.75rem;
    text-transform:uppercase;
    letter-spacing:1px;
    color:var(--yellow);
    font-weight:700;
    margin-bottom:8px;
  }
  .tradeoff-box p{margin:0;line-height:1.6;font-size:0.94rem;}
  .actions-row{
    display:flex;
    justify-content:flex-end;
    margin-top:22px;
    gap:12px;
  }
  .progress-dots{
    display:flex;
    gap:8px;
    margin-bottom:18px;
  }
  .progress-dots .dot{
    width:32px;height:6px;border-radius:4px;
    background:#212c45;
    transition:background 0.3s ease;
  }
  .progress-dots .dot.done{background:var(--green);}
  .progress-dots .dot.active{background:var(--accent);}
  .dashboard-header{
    text-align:center;
    padding:20px 0 30px;
  }
  .score-circle{
    width:180px;height:180px;
    border-radius:50%;
    margin:0 auto 16px;
    display:flex;
    align-items:center;
    justify-content:center;
    flex-direction:column;
    background:conic-gradient(var(--accent) calc(var(--score) * 1%), #1a2338 0);
    position:relative;
  }
  .score-circle::before{
    content:'';
    position:absolute;
    width:148px;height:148px;
    border-radius:50%;
    background:var(--bg);
  }
  .score-circle .score-num{
    position:relative;
    font-size:2.6rem;
    font-weight:800;
  }
  .score-circle .score-sub{
    position:relative;
    font-size:0.8rem;
    color:var(--text-dim);
  }
  .dash-grid{
    display:grid;
    grid-template-columns:repeat(auto-fit,minmax(280px,1fr));
    gap:18px;
    margin-top:10px;
  }
  .dash-grid .card h3{
    margin:0 0 12px;
    font-size:1.05rem;
    display:flex;
    align-items:center;
    gap:8px;
  }
  .dash-grid ul{
    margin:0;padding-left:18px;
    color:var(--text-dim);
    font-size:0.9rem;
    line-height:1.7;
  }
  .dash-grid ul li{margin-bottom:4px;}
  .recap-list{
    display:flex;
    flex-direction:column;
    gap:10px;
  }
  .recap-item{
    display:flex;
    justify-content:space-between;
    background:#0f1626;
    border:1px solid var(--border);
    border-radius:10px;
    padding:10px 14px;
    font-size:0.85rem;
  }
  .recap-item .k{color:var(--text-dim);}
  .recap-item .v{font-weight:600;color:#a9c2ff;}
  .footer-actions{
    display:flex;
    justify-content:center;
    margin-top:36px;
  }
  h1,h2,h3,h4{font-family:inherit;}
  .risk-banner{
    background:linear-gradient(135deg,#3a1420,#1a0f18);
    border:1px solid #5c2a38;
    border-radius:14px;
    padding:16px 20px;
    margin-top:18px;
    display:flex;
    align-items:center;
    gap:14px;
  }
  .risk-banner .icon{font-size:1.8rem;}
  .risk-banner .text b{color:var(--red);}
</style>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
const { useState, useMemo } = React;

/* ---------------- Data ---------------- */

const METRIC_INFO = {
  cost:          { label: 'Cost Efficiency',        icon: '💰' },
  speed:         { label: 'Delivery Speed',         icon: '🚚' },
  risk:          { label: 'Risk Resilience',        icon: '🛡️' },
  satisfaction:  { label: 'Customer Satisfaction',  icon: '😊' },
  sustainability:{ label: 'Sustainability',         icon: '🌱' },
};

const INDUSTRIES = [
  { name: 'Electronics',      icon: '📱', products: ['Smartphones','Laptops','Wireless Earbuds','Smart Watches'] },
  { name: 'Fashion',          icon: '👗', products: ['T-Shirts','Sneakers','Jackets','Handbags'] },
  { name: 'Food & Beverage',  icon: '🍫', products: ['Chocolate Bars','Bottled Beverages','Snack Packs','Coffee Blends'] },
  { name: 'Furniture',        icon: '🛋️', products: ['Sofas','Office Chairs','Dining Tables','Bookshelves'] },
  { name: 'Pharmaceuticals',  icon: '💊', products: ['Pain Relief Tablets','Vitamins','First-Aid Kits','Medical Masks'] },
];

const COUNTRIES = ['United States','Germany','Japan','Brazil','India','United Kingdom','Australia','South Africa','Canada','Mexico','France','South Korea'];
const DEMAND_LEVELS = ['Low','Medium','High'];
const NAME_PARTS_A = ['Nova','Vertex','Orbit','Summit','Pioneer','Horizon','Zenith','Atlas','Bright','Nexus','Cascade','Meridian'];
const NAME_PARTS_B = ['Co','Industries','Group','Corp','Goods','Works','Supply Co.'];

function rand(n){ return Math.floor(Math.random() * n); }
function shuffle(arr){
  const a = [...arr];
  for(let i=a.length-1;i>0;i--){
    const j = rand(i+1);
    [a[i],a[j]] = [a[j],a[i]];
  }
  return a;
}

function generateCompany(){
  const industry = INDUSTRIES[rand(INDUSTRIES.length)];
  const product = industry.products[rand(industry.products.length)];
  const countries = shuffle(COUNTRIES).slice(0, 3 + rand(3));
  const demand = DEMAND_LEVELS[rand(DEMAND_LEVELS.length)];
  const name = `${NAME_PARTS_A[rand(NAME_PARTS_A.length)]} ${NAME_PARTS_B[rand(NAME_PARTS_B.length)]}`;
  return { name, industry: industry.name, icon: industry.icon, product, countries, demand };
}

const DECISIONS = [
  {
    key: 'suppliers',
    title: 'Choose Your Supplier Strategy',
    concept: {
      what: 'A supplier is the business that provides the raw materials or components you need to make your product.',
      why: 'How many suppliers you rely on directly affects your cost and your exposure to disruption.',
      how: 'Fewer suppliers can mean better prices, but if something goes wrong with your only supplier, your entire operation can stop.',
    },
    options: [
      {
        id: 'single',
        label: 'Single Supplier',
        short: 'Work with one trusted supplier for all your materials.',
        tradeoff: 'You gain lower costs thanks to bulk pricing and a simpler relationship to manage — but you create a single point of failure. If that supplier faces a strike, shortage, or shutdown, your entire supply chain stalls.',
        effects: { cost: 10, speed: 0, risk: -20, satisfaction: -5, sustainability: 0 },
      },
      {
        id: 'multiple',
        label: 'Multiple Suppliers',
        short: 'Split your orders across 2–3 suppliers in different regions.',
        tradeoff: 'This costs more to manage and you lose some bulk-discount leverage — but it protects you through risk diversification. If one supplier fails, the others keep you running.',
        effects: { cost: -10, speed: 0, risk: 20, satisfaction: 5, sustainability: -5 },
      },
    ],
  },
  {
    key: 'factory',
    title: 'Choose Your Factory Location',
    concept: {
      what: 'Your factory (or manufacturing partner) is where raw materials become the finished product customers buy.',
      why: 'Location determines your labor costs, shipping distances, and how fast you can respond to demand changes.',
      how: 'Factories close to your customers are fast and reliable but expensive to run. Factories far away are cheap to run but slow to ship from.',
    },
    options: [
      {
        id: 'domestic',
        label: 'Domestic Factory',
        short: 'Build your product in your home market.',
        tradeoff: 'Labor and operating costs are higher, but you get fast delivery, tighter quality control, and a smaller environmental footprint from shipping.',
        effects: { cost: -10, speed: 15, risk: 10, satisfaction: 10, sustainability: 10 },
      },
      {
        id: 'nearshore',
        label: 'Nearshore Factory',
        short: 'Build in a neighboring country, closer to home.',
        tradeoff: 'A balanced middle ground: moderate costs, reasonably fast shipping, and manageable risk — no extreme trade-offs in either direction.',
        effects: { cost: 5, speed: 5, risk: 5, satisfaction: 5, sustainability: 5 },
      },
      {
        id: 'offshore',
        label: 'Offshore Factory',
        short: 'Build in a low-cost country overseas.',
        tradeoff: 'This is the cheapest way to manufacture, but shipping takes much longer, geopolitical and customs risk rises, and the carbon footprint grows significantly.',
        effects: { cost: 20, speed: -15, risk: -10, satisfaction: -5, sustainability: -15 },
      },
    ],
  },
  {
    key: 'warehouse',
    title: 'Choose Your Warehouse Strategy',
    concept: {
      what: 'A warehouse stores your finished goods until a customer orders them.',
      why: 'Where — and how much — you store determines how quickly you can fulfill orders and how much you spend on storage.',
      how: 'Centralizing storage in one place is cheap to run but slow to reach distant customers. Spreading storage across regions speeds up delivery but raises costs.',
    },
    options: [
      {
        id: 'centralized',
        label: 'Centralized Warehouse',
        short: 'One large warehouse serving all markets.',
        tradeoff: 'This is the cheapest way to store inventory, but products must travel farther to reach distant customers, which slows delivery.',
        effects: { cost: 15, speed: -10, risk: -5, satisfaction: -5, sustainability: 5 },
      },
      {
        id: 'distributed',
        label: 'Distributed Warehouses',
        short: 'Several smaller warehouses placed near customers.',
        tradeoff: 'Delivery becomes much faster and customers are happier, but you pay more to operate multiple sites and emissions rise slightly from extra facilities.',
        effects: { cost: -15, speed: 20, risk: 10, satisfaction: 15, sustainability: -5 },
      },
      {
        id: 'jit',
        label: 'Just-in-Time (Minimal Storage)',
        short: 'Store almost nothing; produce as orders arrive.',
        tradeoff: 'Very cheap to run and great for sustainability, but with almost no buffer stock, even a small disruption anywhere in the chain delays every order.',
        effects: { cost: 10, speed: -5, risk: -15, satisfaction: -5, sustainability: 10 },
      },
    ],
  },
  {
    key: 'transport',
    title: 'Choose Your Transportation Method',
    concept: {
      what: 'Transportation moves goods between your suppliers, factories, warehouses, and customers.',
      why: 'The mode you choose is one of the biggest levers on both cost and delivery speed.',
      how: 'Air is fast but expensive and pollutes more. Sea is cheap but slow. Road and rail sit in between, each with their own strengths.',
    },
    options: [
      {
        id: 'road',
        label: 'Road Freight',
        short: 'Trucks moving goods over land.',
        tradeoff: 'Reliable and flexible for short-to-medium distances, with moderate cost, speed, and emissions — a dependable all-rounder.',
        effects: { cost: 5, speed: 5, risk: 5, satisfaction: 0, sustainability: -5 },
      },
      {
        id: 'rail',
        label: 'Rail Freight',
        short: 'Trains carrying large volumes over land.',
        tradeoff: 'Efficient and eco-friendly for bulk goods, but slower and less flexible since it depends on fixed rail routes.',
        effects: { cost: 10, speed: -5, risk: 0, satisfaction: -5, sustainability: 15 },
      },
      {
        id: 'sea',
        label: 'Sea Freight',
        short: 'Cargo ships crossing oceans.',
        tradeoff: 'The cheapest way to move huge volumes of goods, but by far the slowest — often weeks instead of days.',
        effects: { cost: 20, speed: -20, risk: -5, satisfaction: -10, sustainability: 10 },
      },
      {
        id: 'air',
        label: 'Air Freight',
        short: 'Cargo planes for urgent shipments.',
        tradeoff: 'The fastest option by far, which delights customers, but it is very expensive and has the largest carbon footprint of any mode.',
        effects: { cost: -20, speed: 25, risk: 5, satisfaction: 15, sustainability: -20 },
      },
    ],
  },
  {
    key: 'inventory',
    title: 'Choose Your Inventory Strategy',
    concept: {
      what: 'Inventory strategy is how much stock you keep on hand before it sells.',
      why: 'Holding stock ties up cash and space, but running out of stock costs you sales and customer trust.',
      how: 'Lean inventory frees up cash but risks stockouts. Heavy inventory protects against surprises but ties up capital that could be used elsewhere.',
    },
    options: [
      {
        id: 'low',
        label: 'Low Inventory (Lean)',
        short: 'Keep minimal stock and restock frequently.',
        tradeoff: 'This frees up cash and warehouse space, but a sudden demand spike or a shipping delay can quickly cause stockouts and lost sales.',
        effects: { cost: 15, speed: -5, risk: -15, satisfaction: -10, sustainability: 5 },
      },
      {
        id: 'balanced',
        label: 'Balanced Inventory',
        short: 'Keep a moderate, data-informed stock level.',
        tradeoff: 'A steady middle ground that avoids the extremes of overstocking and stockouts, giving predictable, stable performance.',
        effects: { cost: 0, speed: 0, risk: 5, satisfaction: 5, sustainability: 0 },
      },
      {
        id: 'high',
        label: 'High Inventory (Safety Stock)',
        short: 'Keep a large buffer of stock at all times.',
        tradeoff: 'Excellent protection against disruptions and stockouts, but it ties up significant cash and storage space that could otherwise grow the business.',
        effects: { cost: -15, speed: 5, risk: 15, satisfaction: 10, sustainability: -5 },
      },
    ],
  },
];

const IMPROVEMENT_TEXT = {
  cost: 'Renegotiate supplier contracts or consolidate shipments to improve cost efficiency.',
  speed: 'Add a regional warehouse or a faster transport lane to cut delivery times.',
  risk: 'Diversify your suppliers or build safety stock to reduce exposure to disruptions.',
  satisfaction: 'Invest in faster fulfillment or better inventory availability to boost satisfaction.',
  sustainability: 'Shift toward rail or sea freight, or source locally, to lower your carbon footprint.',
};

function clamp(v){ return Math.max(0, Math.min(100, v)); }

function barColor(value){
  if (value >= 70) return 'var(--green)';
  if (value >= 40) return 'var(--yellow)';
  return 'var(--red)';
}

/* ---------------- Components ---------------- */

function MetricsPanel({ metrics }){
  return (
    <div className="card metrics-panel">
      <h3 style={{margin:'0 0 14px', fontSize:'1.05rem'}}>📊 Live Business Metrics</h3>
      {Object.keys(METRIC_INFO).map(key => {
        const info = METRIC_INFO[key];
        const val = Math.round(metrics[key]);
        return (
          <div className="metric-row" key={key}>
            <div className="metric-label">
              <span>{info.icon} {info.label}</span>
              <span className="value">{val}</span>
            </div>
            <div className="bar-track">
              <div className="bar-fill" style={{ width: val + '%', background: barColor(val) }}></div>
            </div>
          </div>
        );
      })}
    </div>
  );
}

function Welcome({ onStart }){
  return (
    <div className="card welcome-hero">
      <h1>🔗 Supply Chain Builder</h1>
      <p>
        A supply chain is every step it takes to get a product from raw materials into a
        customer's hands — sourcing, manufacturing, storing, and shipping. Every decision
        along the way involves a trade-off between cost, speed, risk, customer happiness,
        and sustainability. In this simulation, you'll run a randomly generated company and
        build its supply chain step by step, learning what each choice really means before
        you make it.
      </p>
      <div className="info-grid">
        <div className="card">
          <h3>💰 Cost</h3>
          <p>How efficiently you spend money to get your product made and delivered.</p>
        </div>
        <div className="card">
          <h3>🚚 Speed</h3>
          <p>How quickly a product moves from factory to customer's doorstep.</p>
        </div>
        <div className="card">
          <h3>🛡️ Risk</h3>
          <p>How well your supply chain survives disruptions like delays or shortages.</p>
        </div>
        <div className="card">
          <h3>😊 Satisfaction</h3>
          <p>How happy customers are with availability, speed, and reliability.</p>
        </div>
      </div>
      <button className="btn" onClick={onStart}>Start Building →</button>
    </div>
  );
}

function CompanyReveal({ company, onBegin }){
  return (
    <div className="card">
      <div className="company-card">
        <div className="company-icon">{company.icon}</div>
        <div className="company-details">
          <h2>{company.name}</h2>
          <div style={{color:'var(--text-dim)', marginBottom:'6px'}}>
            {company.industry} · Flagship product: <b style={{color:'var(--text)'}}>{company.product}</b>
          </div>
          <div>
            <span className="tag">📦 Demand: {company.demand}</span>
            {company.countries.map(c => <span className="tag" key={c}>🌍 {c}</span>)}
          </div>
        </div>
      </div>
      <p style={{color:'var(--text-dim)', marginTop:'20px', lineHeight:1.6}}>
        You are now the Supply Chain Director for <b style={{color:'var(--text)'}}>{company.name}</b>.
        You'll make five key decisions — suppliers, factory location, warehousing, transportation,
        and inventory — and watch how each one shifts your live business metrics. At the end,
        you'll get a full performance dashboard.
      </p>
      <div className="actions-row">
        <button className="btn" onClick={onBegin}>Begin Building →</button>
      </div>
    </div>
  );
}

function StepCard({ step, stepIndex, totalSteps, metrics, onChoose, selectedId, pendingOption, onContinue }){
  return (
    <div className="card">
      <div className="progress-dots">
        {Array.from({length: totalSteps}).map((_, i) => (
          <div key={i} className={'dot ' + (i < stepIndex ? 'done' : i === stepIndex ? 'active' : '')}></div>
        ))}
      </div>
      <div className="step-header">
        <span className="step-badge">Step {stepIndex + 1} of {totalSteps}</span>
      </div>
      <h2 className="step-title">{step.title}</h2>

      <div className="concept-box">
        <div className="row"><b>What it is:</b> {step.concept.what}</div>
        <div className="row"><b>Why it matters:</b> {step.concept.why}</div>
        <div className="row"><b>How it affects your business:</b> {step.concept.how}</div>
      </div>

      <div className="options-grid">
        {step.options.map(opt => (
          <div
            key={opt.id}
            className={'option-card' + (selectedId === opt.id ? ' selected' : '')}
            onClick={() => onChoose(opt)}
          >
            <h4>{opt.label}</h4>
            <p className="short">{opt.short}</p>
          </div>
        ))}
      </div>

      {pendingOption && (
        <div className="tradeoff-box">
          <div className="label">⚖️ Trade-off: {pendingOption.label}</div>
          <p>{pendingOption.tradeoff}</p>
        </div>
      )}

      <div className="actions-row">
        <button className="btn" disabled={!pendingOption} onClick={onContinue}>
          {stepIndex === totalSteps - 1 ? 'Finish & See Dashboard →' : 'Continue →'}
        </button>
      </div>
    </div>
  );
}

function computeDashboard(metrics, company, choices){
  const keys = Object.keys(METRIC_INFO);
  const overall = Math.round(keys.reduce((sum, k) => sum + metrics[k], 0) / keys.length);

  const strengths = keys.filter(k => metrics[k] >= 70);
  const weaknesses = keys.filter(k => metrics[k] <= 40);

  let biggestRiskKey = keys[0];
  keys.forEach(k => { if (metrics[k] < metrics[biggestRiskKey]) biggestRiskKey = k; });

  const sortedByLow = [...keys].sort((a,b) => metrics[a] - metrics[b]);
  const improvements = sortedByLow.slice(0, 3).map(k => IMPROVEMENT_TEXT[k]);

  return { overall, strengths, weaknesses, biggestRiskKey, improvements };
}

function Dashboard({ company, metrics, choices, onReplay }){
  const { overall, strengths, weaknesses, biggestRiskKey, improvements } = useMemo(
    () => computeDashboard(metrics, company, choices),
    [metrics, company, choices]
  );

  return (
    <div>
      <div className="card dashboard-header">
        <div className="step-badge">Final Report</div>
        <h2 style={{fontSize:'1.7rem', margin:'8px 0 4px'}}>{company.name}'s Supply Chain</h2>
        <p style={{color:'var(--text-dim)', margin:'0 0 20px'}}>Overall Supply Chain Score</p>
        <div className="score-circle" style={{'--score': overall}}>
          <div className="score-num">{overall}</div>
          <div className="score-sub">out of 100</div>
        </div>

        <div className="risk-banner">
          <div className="icon">⚠️</div>
          <div className="text">
            Biggest Risk: <b>{METRIC_INFO[biggestRiskKey].label}</b> is your weakest area at {Math.round(metrics[biggestRiskKey])}/100.
            This is the part of your supply chain most likely to cause problems if left unaddressed.
          </div>
        </div>
      </div>

      <div className="dash-grid">
        <div className="card">
          <h3>💪 Strengths</h3>
          {strengths.length ? (
            <ul>{strengths.map(k => <li key={k}>{METRIC_INFO[k].icon} {METRIC_INFO[k].label} — {Math.round(metrics[k])}/100</li>)}</ul>
          ) : (
            <p style={{color:'var(--text-dim)', fontSize:'0.9rem'}}>No standout strengths yet — every area has room to grow.</p>
          )}
        </div>

        <div className="card">
          <h3>🧩 Weaknesses</h3>
          {weaknesses.length ? (
            <ul>{weaknesses.map(k => <li key={k}>{METRIC_INFO[k].icon} {METRIC_INFO[k].label} — {Math.round(metrics[k])}/100</li>)}</ul>
          ) : (
            <p style={{color:'var(--text-dim)', fontSize:'0.9rem'}}>No critical weaknesses — a well-balanced supply chain.</p>
          )}
        </div>

        <div className="card">
          <h3>🚀 Three Practical Improvements</h3>
          <ul>
            {improvements.map((imp, i) => <li key={i}>{imp}</li>)}
          </ul>
        </div>

        <div className="card">
          <h3>📋 Your Decisions</h3>
          <div className="recap-list">
            {DECISIONS.map(step => (
              <div className="recap-item" key={step.key}>
                <span className="k">{step.title.replace('Choose Your ','')}</span>
                <span className="v">{choices[step.key] ? choices[step.key].label : '-'}</span>
              </div>
            ))}
          </div>
        </div>
      </div>

      <div className="footer-actions">
        <button className="btn" onClick={onReplay}>🔄 Replay with a New Company</button>
      </div>
    </div>
  );
}

function App(){
  const [screen, setScreen] = useState('welcome'); // welcome | company | building | dashboard
  const [company, setCompany] = useState(null);
  const [stepIndex, setStepIndex] = useState(0);
  const [choices, setChoices] = useState({});
  const [pendingOption, setPendingOption] = useState(null);
  const [metrics, setMetrics] = useState({ cost:50, speed:50, risk:50, satisfaction:50, sustainability:50 });

  function resetAll(){
    setCompany(generateCompany());
    setStepIndex(0);
    setChoices({});
    setPendingOption(null);
    setMetrics({ cost:50, speed:50, risk:50, satisfaction:50, sustainability:50 });
    setScreen('company');
  }

  function handleStart(){
    resetAll();
  }

  function handleBegin(){
    setScreen('building');
  }

  function handleChoose(option){
    setPendingOption(option);
  }

  function handleContinue(){
    const step = DECISIONS[stepIndex];
    const newMetrics = { ...metrics };
    Object.keys(pendingOption.effects).forEach(k => {
      newMetrics[k] = clamp(newMetrics[k] + pendingOption.effects[k]);
    });
    setMetrics(newMetrics);
    setChoices({ ...choices, [step.key]: pendingOption });
    setPendingOption(null);

    if (stepIndex === DECISIONS.length - 1){
      setScreen('dashboard');
    } else {
      setStepIndex(stepIndex + 1);
    }
  }

  function handleReplay(){
    resetAll();
    setScreen('company');
  }

  return (
    <div className="app-shell">
      <div className="topbar">
        <div className="brand"><span className="dot"></span> Supply Chain Builder</div>
        {company && screen !== 'welcome' && (
          <div style={{color:'var(--text-dim)', fontSize:'0.85rem'}}>
            {company.icon} {company.name}
          </div>
        )}
      </div>

      {screen === 'welcome' && <Welcome onStart={handleStart} />}

      {screen === 'company' && company && (
        <CompanyReveal company={company} onBegin={handleBegin} />
      )}

      {screen === 'building' && company && (
        <div className="layout">
          <StepCard
            step={DECISIONS[stepIndex]}
            stepIndex={stepIndex}
            totalSteps={DECISIONS.length}
            metrics={metrics}
            onChoose={handleChoose}
            selectedId={pendingOption ? pendingOption.id : null}
            pendingOption={pendingOption}
            onContinue={handleContinue}
          />
          <MetricsPanel metrics={metrics} />
        </div>
      )}

      {screen === 'dashboard' && company && (
        <Dashboard company={company} metrics={metrics} choices={choices} onReplay={handleReplay} />
      )}
    </div>
  );
}

ReactDOM.createRoot(document.getElementById('root')).render(<App />);
</script>
</body>
</html>
```
