import { useState, useEffect, useRef } from "react";

// ─── CONSTANTS ───────────────────────────────────────────────────────────────
const BRAND = {
  name: "Chicken Town",
  tagline: "Freetown's Favourite Crunch",
  phone: "+232 76 000 000",
  email: "hello@chickentown.sl",
  whatsapp: "https://wa.me/23276000000",
};

const LOCATIONS = [
  {
    id: 1,
    name: "Chicken Town — Wilberforce",
    address: "14 Wilberforce Street, Freetown",
    hours: "Mon–Sun: 9:00 AM – 11:00 PM",
    phone: "+232 76 100 001",
    zone: 1,
  },
  {
    id: 2,
    name: "Chicken Town — Aberdeen",
    address: "Aberdeen Road, Near Lighthouse, Freetown",
    hours: "Mon–Sun: 10:00 AM – 10:00 PM",
    phone: "+232 76 100 002",
    zone: 2,
  },
  {
    id: 3,
    name: "Chicken Town — Lumley",
    address: "Lumley Beach Road, Freetown",
    hours: "Mon–Sun: 9:00 AM – 12:00 AM",
    phone: "+232 76 100 003",
    zone: 2,
  },
  {
    id: 4,
    name: "Chicken Town — Bo Junction",
    address: "Wellington Industrial Estate, Freetown",
    hours: "Mon–Fri: 8:00 AM – 9:00 PM",
    phone: "+232 76 100 004",
    zone: 3,
  },
];

const DELIVERY_ZONES = [
  { zone: 1, label: "Zone 1 — Central Freetown", fee: 5000, areas: "Wilberforce, Tower Hill, State House area" },
  { zone: 2, label: "Zone 2 — West & Coastal", fee: 10000, areas: "Aberdeen, Lumley, Hill Station, Tengeh" },
  { zone: 3, label: "Zone 3 — East & Outskirts", fee: 15000, areas: "Wellington, Kissy, Waterloo, Grafton" },
];

const MENU = {
  "Chicken Meals": [
    { id: 1, name: "Signature Crispy Chicken", desc: "Juicy whole-leg fried chicken with our secret 11-spice crust", price: 45000, emoji: "🍗", badge: "Best Seller" },
    { id: 2, name: "Spicy Fire Thighs", desc: "Fiery marinated thighs, deep-fried golden & tossed in chili glaze", price: 40000, emoji: "🔥", badge: "Hot" },
    { id: 3, name: "Grilled Herb Chicken", desc: "Chargrilled chicken breast with lemon-herb seasoning & garlic sauce", price: 50000, emoji: "🍽️", badge: null },
    { id: 4, name: "Chicken Strips (6pc)", desc: "Tender chicken strips with choice of dipping sauce", price: 38000, emoji: "🍗", badge: null },
  ],
  "Burgers": [
    { id: 5, name: "CT Classic Burger", desc: "Crispy chicken fillet, lettuce, tomato, mayo & pickles in a toasted bun", price: 35000, emoji: "🍔", badge: "Fan Fave" },
    { id: 6, name: "Double Stack Burger", desc: "Two crispy fillets, double cheese, caramelised onion & CT sauce", price: 48000, emoji: "🍔", badge: null },
    { id: 7, name: "Spicy BBQ Burger", desc: "Spiced fillet, smoky BBQ sauce, jalapeños & coleslaw", price: 42000, emoji: "🌶️", badge: null },
  ],
  "Wraps": [
    { id: 8, name: "Grilled Chicken Wrap", desc: "Soft tortilla with grilled strips, fresh veg, garlic aioli", price: 32000, emoji: "🌯", badge: null },
    { id: 9, name: "Spicy Crunch Wrap", desc: "Crispy chicken, sriracha drizzle, lettuce, cheese & tomato", price: 34000, emoji: "🌯", badge: "New" },
  ],
  "Combos": [
    { id: 10, name: "Family Feast (4 pcs)", desc: "4 pieces crispy chicken + large fries + 4 drinks + coleslaw", price: 160000, emoji: "👨‍👩‍👧‍👦", badge: "Value" },
    { id: 11, name: "Solo Meal Deal", desc: "1 pc chicken + regular fries + drink + dip sauce", price: 55000, emoji: "🎯", badge: "Value" },
    { id: 12, name: "Couples Combo", desc: "2 burgers + 2 drinks + shared fries", price: 90000, emoji: "💑", badge: null },
  ],
  "Sides": [
    { id: 13, name: "Crispy Fries", desc: "Golden seasoned fries — regular or large", price: 18000, emoji: "🍟", badge: null },
    { id: 14, name: "Coleslaw Bowl", desc: "Creamy homemade coleslaw, fresh-cut daily", price: 12000, emoji: "🥗", badge: null },
    { id: 15, name: "Jollof Rice Side", desc: "West African jollof rice, slow-cooked with tomatoes & spices", price: 20000, emoji: "🍚", badge: "Local Fave" },
    { id: 16, name: "Corn on the Cob", desc: "Grilled sweetcorn with butter & seasoning", price: 10000, emoji: "🌽", badge: null },
  ],
  "Drinks": [
    { id: 17, name: "Soft Drinks", desc: "Pepsi, 7UP, Mirinda, Tonic — chilled bottles", price: 8000, emoji: "🥤", badge: null },
    { id: 18, name: "Fresh Fruit Juice", desc: "Daily fresh-squeezed mango, pineapple, or orange", price: 15000, emoji: "🍊", badge: "Fresh" },
    { id: 19, name: "Chilled Water (500ml)", desc: "Ice cold bottled water", price: 5000, emoji: "💧", badge: null },
    { id: 20, name: "Milkshake", desc: "Thick vanilla, chocolate or strawberry milkshake", price: 22000, emoji: "🥛", badge: null },
  ],
};

const TESTIMONIALS = [
  { name: "Aminata K.", text: "Best crispy chicken in Freetown! The spicy fire thighs are unreal 🔥", rating: 5 },
  { name: "Mohamed S.", text: "Clean restaurant, fast service, and the combo deals are great value for money.", rating: 5 },
  { name: "Fatmata B.", text: "The jollof rice side dish takes me back home. Chicken Town gets it right.", rating: 5 },
  { name: "Ibrahim C.", text: "Ordered for delivery — arrived hot and well-packed. Will order again!", rating: 4 },
];

const FAQS = [
  { q: "How do I place an order?", a: "You can order directly on this website, via WhatsApp, or visit any of our branches. Click 'Order Now' to get started." },
  { q: "Do you deliver across Freetown?", a: "Yes! We deliver across Freetown in 3 zones. Delivery fees range from Le 5,000 to Le 15,000 depending on your area." },
  { q: "How long does delivery take?", a: "Typical delivery is 30–60 minutes depending on your zone and time of day. We'll keep you updated via WhatsApp." },
  { q: "Can I order as a guest?", a: "Absolutely. You can browse the menu and place an order without creating an account." },
  { q: "What payment methods do you accept?", a: "We accept cash on delivery, Orange Money, Africell Money, and bank transfers. Card payments coming soon." },
  { q: "Are your chickens halal?", a: "Yes. All our chicken is sourced from certified halal suppliers." },
];

// ─── HELPERS ─────────────────────────────────────────────────────────────────
const fmt = (n) => `Le ${n.toLocaleString()}`;

// ─── COMPONENTS ──────────────────────────────────────────────────────────────

function StarRating({ n }) {
  return <span className="text-yellow-400">{"★".repeat(n)}{"☆".repeat(5 - n)}</span>;
}

function SocialBar({ className = "" }) {
  const socials = [
    { label: "Facebook", icon: "f", color: "#1877F2", href: "#" },
    { label: "Instagram", icon: "▶", color: "#E1306C", href: "#" },
    { label: "TikTok", icon: "♪", color: "#000", href: "#" },
    { label: "WhatsApp", icon: "✉", color: "#25D366", href: BRAND.whatsapp },
  ];
  return (
    <div className={`flex gap-3 ${className}`}>
      {socials.map((s) => (
        <a key={s.label} href={s.href} target="_blank" rel="noreferrer"
          title={s.label}
          style={{ background: s.color }}
          className="w-9 h-9 rounded-full flex items-center justify-center text-white text-sm font-bold hover:scale-110 transition-transform shadow-md">
          {s.icon}
        </a>
      ))}
    </div>
  );
}

// ─── SPLASH ──────────────────────────────────────────────────────────────────
function Splash({ onDone }) {
  const [progress, setProgress] = useState(0);
  const [fadeOut, setFadeOut] = useState(false);

  useEffect(() => {
    const timer = setInterval(() => {
      setProgress((p) => {
        if (p >= 100) { clearInterval(timer); return 100; }
        return p + 4;
      });
    }, 60);
    return () => clearInterval(timer);
  }, []);

  useEffect(() => {
    if (progress >= 100) {
      setTimeout(() => { setFadeOut(true); setTimeout(onDone, 600); }, 300);
    }
  }, [progress, onDone]);

  return (
    <div className={`fixed inset-0 z-50 flex flex-col items-center justify-center transition-opacity duration-600 ${fadeOut ? "opacity-0" : "opacity-100"}`}
      style={{ background: "linear-gradient(135deg, #C0392B 0%, #E74C3C 40%, #F39C12 100%)" }}>
      {/* Logo */}
      <div className="flex flex-col items-center mb-10 animate-pulse">
        <div className="w-28 h-28 rounded-full bg-white shadow-2xl flex items-center justify-center mb-4"
          style={{ boxShadow: "0 0 60px rgba(255,255,255,0.4)" }}>
          <span className="text-6xl">🍗</span>
        </div>
        <h1 className="text-white font-black text-4xl tracking-tight" style={{ fontFamily: "Georgia, serif", letterSpacing: "-1px" }}>
          CHICKEN<span className="text-yellow-300"> TOWN</span>
        </h1>
        <p className="text-white/80 text-sm mt-1 tracking-widest uppercase">{BRAND.tagline}</p>
      </div>

      {/* Progress bar */}
      <div className="w-56 h-1.5 rounded-full bg-white/20 overflow-hidden">
        <div className="h-full rounded-full bg-yellow-300 transition-all duration-100"
          style={{ width: `${progress}%` }} />
      </div>
      <p className="text-white/60 text-xs mt-3 tracking-widest">LOADING…</p>
    </div>
  );
}

// ─── AUTH MODAL ──────────────────────────────────────────────────────────────
function AuthModal({ onAuth }) {
  const [mode, setMode] = useState("choice"); // choice | login | signup
  const [form, setForm] = useState({ name: "", email: "", phone: "", password: "" });

  const submit = (e) => {
    e.preventDefault();
    onAuth({ name: form.name || form.email.split("@")[0], email: form.email, isGuest: false });
  };

  return (
    <div className="fixed inset-0 z-40 flex items-center justify-center p-4"
      style={{ background: "rgba(0,0,0,0.7)", backdropFilter: "blur(6px)" }}>
      <div className="bg-white rounded-3xl shadow-2xl w-full max-w-sm overflow-hidden">
        {/* Header */}
        <div className="p-6 text-center" style={{ background: "linear-gradient(135deg,#C0392B,#E74C3C)" }}>
          <div className="text-4xl mb-2">🍗</div>
          <h2 className="text-white font-black text-xl">CHICKEN TOWN</h2>
          <p className="text-white/80 text-sm">{BRAND.tagline}</p>
        </div>

        <div className="p-6">
          {mode === "choice" && (
            <div className="space-y-3">
              <h3 className="text-center font-bold text-gray-800 text-lg mb-4">Welcome back! 👋</h3>
              <button onClick={() => setMode("login")}
                className="w-full py-3 rounded-2xl font-bold text-white text-sm transition-all hover:scale-[1.02] active:scale-95"
                style={{ background: "#C0392B" }}>
                Log In to My Account
              </button>
              <button onClick={() => setMode("signup")}
                className="w-full py-3 rounded-2xl font-bold text-sm border-2 transition-all hover:scale-[1.02] active:scale-95"
                style={{ borderColor: "#C0392B", color: "#C0392B" }}>
                Create an Account
              </button>
              <div className="relative my-2">
                <div className="absolute inset-0 flex items-center"><div className="w-full border-t border-gray-200" /></div>
                <div className="relative flex justify-center"><span className="bg-white px-3 text-xs text-gray-400">or</span></div>
              </div>
              <button onClick={() => onAuth({ name: "Guest", isGuest: true })}
                className="w-full py-3 rounded-2xl font-semibold text-gray-600 text-sm bg-gray-100 transition-all hover:bg-gray-200 hover:scale-[1.02] active:scale-95">
                Continue as Guest 👀
              </button>
              <p className="text-center text-xs text-gray-400 mt-2">No account needed to browse or order</p>
            </div>
          )}

          {(mode === "login" || mode === "signup") && (
            <form onSubmit={submit} className="space-y-3">
              <button type="button" onClick={() => setMode("choice")}
                className="text-sm text-gray-400 hover:text-gray-600 flex items-center gap-1 mb-2">
                ← Back
              </button>
              <h3 className="font-bold text-gray-800 text-lg">{mode === "login" ? "Log In" : "Create Account"}</h3>

              {mode === "signup" && (
                <>
                  <input required placeholder="Full Name" value={form.name}
                    onChange={e => setForm({ ...form, name: e.target.value })}
                    className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
                  <input placeholder="Phone Number" value={form.phone}
                    onChange={e => setForm({ ...form, phone: e.target.value })}
                    className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
                </>
              )}
              <input required type="email" placeholder="Email Address" value={form.email}
                onChange={e => setForm({ ...form, email: e.target.value })}
                className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
              <input required type="password" placeholder="Password" value={form.password}
                onChange={e => setForm({ ...form, password: e.target.value })}
                className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />

              <button type="submit"
                className="w-full py-3 rounded-2xl font-bold text-white text-sm transition-all hover:scale-[1.02] active:scale-95"
                style={{ background: "#C0392B" }}>
                {mode === "login" ? "Log In →" : "Create Account →"}
              </button>
              <p className="text-center text-xs text-gray-400">
                {mode === "login" ? "No account? " : "Already have one? "}
                <button type="button" className="text-red-600 font-semibold"
                  onClick={() => setMode(mode === "login" ? "signup" : "login")}>
                  {mode === "login" ? "Sign Up" : "Log In"}
                </button>
              </p>
            </form>
          )}
        </div>
      </div>
    </div>
  );
}

// ─── NAVBAR ──────────────────────────────────────────────────────────────────
function Navbar({ user, onLogout, cartCount, setPage, page, setShowCart }) {
  const [menuOpen, setMenuOpen] = useState(false);
  const navItems = ["Home", "Menu", "Locations", "About", "Contact"];

  return (
    <nav className="fixed top-0 left-0 right-0 z-30 shadow-lg"
      style={{ background: "#1a0a00" }}>
      <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
        {/* Logo */}
        <button onClick={() => { setPage("home"); setMenuOpen(false); }}
          className="flex items-center gap-2 group">
          <span className="text-2xl">🍗</span>
          <span className="text-white font-black text-lg tracking-tight" style={{ fontFamily: "Georgia, serif" }}>
            CHICKEN<span className="text-yellow-400"> TOWN</span>
          </span>
        </button>

        {/* Desktop nav */}
        <div className="hidden md:flex items-center gap-6">
          {navItems.map((item) => (
            <button key={item}
              onClick={() => setPage(item.toLowerCase())}
              className={`text-sm font-semibold transition-colors ${page === item.toLowerCase() ? "text-yellow-400" : "text-white/70 hover:text-white"}`}>
              {item}
            </button>
          ))}
        </div>

        {/* Right side */}
        <div className="flex items-center gap-3">
          <button onClick={() => setShowCart(true)}
            className="relative p-2 text-white hover:text-yellow-400 transition-colors">
            <span className="text-xl">🛒</span>
            {cartCount > 0 && (
              <span className="absolute -top-1 -right-1 w-5 h-5 rounded-full text-xs font-bold flex items-center justify-center text-white"
                style={{ background: "#E74C3C" }}>{cartCount}</span>
            )}
          </button>

          <div className="hidden md:flex items-center gap-2">
            {user ? (
              <div className="flex items-center gap-2">
                <span className="text-white/70 text-sm">{user.isGuest ? "👋 Guest" : `Hi, ${user.name}`}</span>
                <button onClick={onLogout}
                  className="text-xs text-white/50 hover:text-white border border-white/20 rounded-lg px-2 py-1 transition-colors">
                  {user.isGuest ? "Sign In" : "Log Out"}
                </button>
              </div>
            ) : null}
          </div>

          {/* Mobile menu toggle */}
          <button className="md:hidden text-white text-xl" onClick={() => setMenuOpen(!menuOpen)}>
            {menuOpen ? "✕" : "☰"}
          </button>
        </div>
      </div>

      {/* Mobile menu */}
      {menuOpen && (
        <div className="md:hidden border-t border-white/10" style={{ background: "#1a0a00" }}>
          {navItems.map((item) => (
            <button key={item}
              onClick={() => { setPage(item.toLowerCase()); setMenuOpen(false); }}
              className={`w-full text-left px-6 py-3 text-sm font-semibold border-b border-white/5 transition-colors ${page === item.toLowerCase() ? "text-yellow-400" : "text-white/80"}`}>
              {item}
            </button>
          ))}
          {user && (
            <div className="px-6 py-3 flex items-center justify-between">
              <span className="text-white/60 text-sm">{user.isGuest ? "Browsing as Guest" : user.name}</span>
              <button onClick={() => { onLogout(); setMenuOpen(false); }}
                className="text-xs text-red-400">{user.isGuest ? "Sign In" : "Log Out"}</button>
            </div>
          )}
        </div>
      )}
    </nav>
  );
}

// ─── CART DRAWER ─────────────────────────────────────────────────────────────
function CartDrawer({ cart, setCart, onClose, setPage }) {
  const total = cart.reduce((s, i) => s + i.price * i.qty, 0);

  const update = (id, delta) => {
    setCart(prev => {
      const next = prev.map(i => i.id === id ? { ...i, qty: i.qty + delta } : i).filter(i => i.qty > 0);
      return next;
    });
  };

  return (
    <div className="fixed inset-0 z-50 flex justify-end">
      <div className="absolute inset-0 bg-black/60" onClick={onClose} />
      <div className="relative w-full max-w-sm bg-white h-full flex flex-col shadow-2xl">
        {/* Header */}
        <div className="p-5 flex items-center justify-between border-b" style={{ background: "#C0392B" }}>
          <h2 className="text-white font-black text-lg">🛒 Your Order</h2>
          <button onClick={onClose} className="text-white/80 hover:text-white text-xl">✕</button>
        </div>

        {/* Items */}
        <div className="flex-1 overflow-y-auto p-4 space-y-3">
          {cart.length === 0 ? (
            <div className="text-center mt-12 text-gray-400">
              <p className="text-4xl mb-3">🛒</p>
              <p className="font-semibold">Your cart is empty</p>
              <p className="text-sm">Add some delicious items!</p>
            </div>
          ) : cart.map(item => (
            <div key={item.id} className="flex items-center gap-3 bg-gray-50 rounded-2xl p-3">
              <span className="text-2xl">{item.emoji}</span>
              <div className="flex-1 min-w-0">
                <p className="font-bold text-gray-800 text-sm truncate">{item.name}</p>
                <p className="text-red-600 text-sm font-semibold">{fmt(item.price)}</p>
              </div>
              <div className="flex items-center gap-2">
                <button onClick={() => update(item.id, -1)}
                  className="w-7 h-7 rounded-full bg-gray-200 flex items-center justify-center text-gray-700 font-bold hover:bg-red-100 transition-colors">−</button>
                <span className="font-bold text-sm w-4 text-center">{item.qty}</span>
                <button onClick={() => update(item.id, 1)}
                  className="w-7 h-7 rounded-full flex items-center justify-center text-white font-bold hover:opacity-80 transition-opacity"
                  style={{ background: "#C0392B" }}>+</button>
              </div>
            </div>
          ))}
        </div>

        {/* Footer */}
        {cart.length > 0 && (
          <div className="p-4 border-t space-y-3">
            <div className="flex justify-between items-center">
              <span className="font-semibold text-gray-600">Subtotal</span>
              <span className="font-black text-lg text-gray-800">{fmt(total)}</span>
            </div>
            <button onClick={() => { onClose(); setPage("checkout"); }}
              className="w-full py-4 rounded-2xl font-black text-white text-sm tracking-wide transition-all hover:scale-[1.02] active:scale-95"
              style={{ background: "linear-gradient(90deg,#C0392B,#E74C3C)" }}>
              Proceed to Checkout →
            </button>
            <button onClick={() => setCart([])}
              className="w-full py-2 text-xs text-gray-400 hover:text-red-500 transition-colors">
              Clear cart
            </button>
          </div>
        )}
      </div>
    </div>
  );
}

// ─── HOME PAGE ───────────────────────────────────────────────────────────────
function HomePage({ setPage, addToCart }) {
  const featured = [
    MENU["Chicken Meals"][0],
    MENU["Burgers"][0],
    MENU["Combos"][0],
    MENU["Sides"][2],
  ];

  return (
    <div>
      {/* Hero */}
      <section className="relative min-h-screen flex items-center justify-center overflow-hidden"
        style={{ background: "linear-gradient(135deg, #1a0a00 0%, #3d0e00 50%, #1a0a00 100%)" }}>
        {/* Decorative circles */}
        <div className="absolute top-20 right-10 w-72 h-72 rounded-full opacity-10"
          style={{ background: "radial-gradient(circle, #F39C12, transparent)" }} />
        <div className="absolute bottom-20 left-10 w-48 h-48 rounded-full opacity-10"
          style={{ background: "radial-gradient(circle, #E74C3C, transparent)" }} />

        <div className="relative z-10 text-center px-6 max-w-3xl mx-auto pt-24 pb-16">
          <div className="inline-block bg-yellow-400/20 text-yellow-300 text-xs font-bold px-4 py-2 rounded-full mb-6 tracking-widest uppercase border border-yellow-400/30">
            🇸🇱 Freetown's Finest
          </div>
          <h1 className="text-white font-black leading-tight mb-6"
            style={{ fontSize: "clamp(2.5rem, 8vw, 5rem)", fontFamily: "Georgia, serif", lineHeight: 1.05 }}>
            Crispy. <span style={{ color: "#F39C12" }}>Bold.</span><br />Unforgettable.
          </h1>
          <p className="text-white/70 text-lg mb-8 max-w-lg mx-auto">
            Sierra Leone's premium fast-food experience. Crafted with the freshest local ingredients, fried to golden perfection.
          </p>
          <div className="flex flex-col sm:flex-row gap-3 justify-center">
            <button onClick={() => setPage("menu")}
              className="px-8 py-4 rounded-2xl font-black text-white text-sm tracking-wide shadow-2xl transition-all hover:scale-105 active:scale-95"
              style={{ background: "linear-gradient(90deg, #C0392B, #E74C3C)" }}>
              🍗 Order Now
            </button>
            <button onClick={() => setPage("menu")}
              className="px-8 py-4 rounded-2xl font-bold text-yellow-400 text-sm border-2 border-yellow-400/50 backdrop-blur-sm transition-all hover:bg-yellow-400/10 hover:scale-105">
              View Full Menu →
            </button>
          </div>
          <div className="mt-12 grid grid-cols-3 gap-4 max-w-xs mx-auto">
            {[["10+", "Menu Items"], ["4", "Locations"], ["★4.9", "Rating"]].map(([n, l]) => (
              <div key={l} className="text-center">
                <div className="text-yellow-400 font-black text-xl">{n}</div>
                <div className="text-white/50 text-xs">{l}</div>
              </div>
            ))}
          </div>
        </div>

        {/* Scroll indicator */}
        <div className="absolute bottom-8 left-1/2 -translate-x-1/2 text-white/40 text-xs flex flex-col items-center gap-1 animate-bounce">
          <span>↓</span>
          <span className="tracking-widest text-[10px]">SCROLL</span>
        </div>
      </section>

      {/* Featured */}
      <section className="py-16 px-4 bg-white">
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-10">
            <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Menu Highlights</span>
            <h2 className="text-3xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>
              Can't Miss These 🔥
            </h2>
          </div>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
            {featured.map((item) => (
              <div key={item.id} className="bg-gray-50 rounded-2xl p-4 hover:shadow-lg transition-all hover:-translate-y-1 group cursor-pointer">
                <div className="text-5xl mb-3 text-center">{item.emoji}</div>
                {item.badge && (
                  <span className="text-[10px] font-bold px-2 py-0.5 rounded-full text-white mb-2 inline-block"
                    style={{ background: "#C0392B" }}>{item.badge}</span>
                )}
                <h3 className="font-bold text-gray-800 text-sm mb-1">{item.name}</h3>
                <p className="text-red-600 font-black text-sm">{fmt(item.price)}</p>
                <button onClick={() => addToCart(item)}
                  className="mt-3 w-full py-2 rounded-xl text-xs font-bold text-white transition-all group-hover:scale-105"
                  style={{ background: "#C0392B" }}>
                  Add to Cart
                </button>
              </div>
            ))}
          </div>
          <div className="text-center mt-8">
            <button onClick={() => setPage("menu")}
              className="px-8 py-3 rounded-2xl font-bold text-sm border-2 border-red-600 text-red-600 hover:bg-red-50 transition-colors">
              See Full Menu →
            </button>
          </div>
        </div>
      </section>

      {/* Why Chicken Town */}
      <section className="py-16 px-4" style={{ background: "#1a0a00" }}>
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-10">
            <span className="text-xs font-bold tracking-widest text-yellow-400 uppercase">Why Choose Us</span>
            <h2 className="text-3xl font-black text-white mt-2" style={{ fontFamily: "Georgia, serif" }}>
              The Chicken Town Difference
            </h2>
          </div>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-6">
            {[
              { icon: "🔥", title: "Always Fresh", desc: "Chicken prepared fresh daily, never frozen" },
              { icon: "⚡", title: "Fast Service", desc: "Ready in minutes — eat in, takeaway or delivery" },
              { icon: "💰", title: "Great Value", desc: "Combo deals and family feasts for every budget" },
              { icon: "🌶️", title: "Bold Flavours", desc: "Our secret spice blend is made right here in Freetown" },
            ].map((f) => (
              <div key={f.title} className="text-center p-5 rounded-2xl" style={{ background: "rgba(255,255,255,0.05)" }}>
                <div className="text-4xl mb-3">{f.icon}</div>
                <h3 className="text-white font-bold text-sm mb-1">{f.title}</h3>
                <p className="text-white/50 text-xs">{f.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* Locations preview */}
      <section className="py-16 px-4 bg-gray-50">
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-10">
            <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Find Us</span>
            <h2 className="text-3xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>
              4 Locations Across Freetown
            </h2>
          </div>
          <div className="grid grid-cols-2 md:grid-cols-4 gap-4">
            {LOCATIONS.map(loc => (
              <div key={loc.id} className="bg-white rounded-2xl p-4 shadow-sm hover:shadow-md transition-shadow">
                <div className="text-2xl mb-2">📍</div>
                <h4 className="font-bold text-gray-800 text-sm">{loc.name.replace("Chicken Town — ", "")}</h4>
                <p className="text-xs text-gray-500 mt-1">{loc.address}</p>
                <p className="text-xs text-green-600 mt-2">● Open Today</p>
              </div>
            ))}
          </div>
          <div className="text-center mt-8">
            <button onClick={() => setPage("locations")}
              className="px-8 py-3 rounded-2xl font-bold text-sm text-white transition-all hover:scale-105"
              style={{ background: "#C0392B" }}>
              View All Locations →
            </button>
          </div>
        </div>
      </section>

      {/* Testimonials */}
      <section className="py-16 px-4 bg-white">
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-10">
            <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Reviews</span>
            <h2 className="text-3xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>
              What Freetown Says ❤️
            </h2>
          </div>
          <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-4">
            {TESTIMONIALS.map((t, i) => (
              <div key={i} className="bg-gray-50 rounded-2xl p-5">
                <StarRating n={t.rating} />
                <p className="text-gray-700 text-sm mt-2 italic">"{t.text}"</p>
                <p className="text-gray-500 text-xs mt-3 font-semibold">— {t.name}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* CTA Banner */}
      <section className="py-12 px-4"
        style={{ background: "linear-gradient(90deg, #C0392B, #E74C3C, #F39C12)" }}>
        <div className="max-w-2xl mx-auto text-center">
          <h2 className="text-white font-black text-3xl mb-3" style={{ fontFamily: "Georgia, serif" }}>
            Hungry? We're Ready. 🍗
          </h2>
          <p className="text-white/80 mb-6">Order now for pickup or delivery across Freetown</p>
          <div className="flex flex-col sm:flex-row gap-3 justify-center">
            <button onClick={() => setPage("menu")}
              className="px-8 py-3 rounded-2xl font-black bg-white text-sm transition-all hover:scale-105"
              style={{ color: "#C0392B" }}>
              Order Online
            </button>
            <a href={BRAND.whatsapp} target="_blank" rel="noreferrer"
              className="px-8 py-3 rounded-2xl font-bold border-2 border-white text-white text-sm transition-all hover:bg-white/10">
              WhatsApp Order
            </a>
          </div>
        </div>
      </section>
    </div>
  );
}

// ─── MENU PAGE ────────────────────────────────────────────────────────────────
function MenuPage({ addToCart }) {
  const categories = Object.keys(MENU);
  const [active, setActive] = useState(categories[0]);

  return (
    <div className="pt-20 pb-16 min-h-screen bg-gray-50">
      <div className="max-w-6xl mx-auto px-4">
        <div className="text-center py-10">
          <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Full Menu</span>
          <h1 className="text-4xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>
            What's Good Today 🍗
          </h1>
          <p className="text-gray-500 mt-2">All prices in Sierra Leonean Leones (Le)</p>
        </div>

        {/* Category tabs */}
        <div className="flex gap-2 overflow-x-auto pb-2 mb-8 scrollbar-hide">
          {categories.map(cat => (
            <button key={cat}
              onClick={() => setActive(cat)}
              className={`flex-shrink-0 px-5 py-2 rounded-full text-sm font-bold transition-all ${active === cat ? "text-white shadow-md scale-105" : "bg-white text-gray-600 hover:bg-gray-100 shadow-sm"}`}
              style={active === cat ? { background: "#C0392B" } : {}}>
              {cat}
            </button>
          ))}
        </div>

        {/* Items grid */}
        <div className="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
          {MENU[active].map(item => (
            <div key={item.id} className="bg-white rounded-2xl p-5 shadow-sm hover:shadow-lg transition-all hover:-translate-y-1 flex flex-col">
              <div className="flex items-start justify-between mb-3">
                <span className="text-5xl">{item.emoji}</span>
                {item.badge && (
                  <span className="text-[10px] font-black px-2 py-1 rounded-full text-white"
                    style={{ background: item.badge === "Hot" || item.badge === "New" ? "#E74C3C" : "#F39C12", color: item.badge === "Value" ? "#1a0a00" : "white" }}>
                    {item.badge}
                  </span>
                )}
              </div>
              <h3 className="font-black text-gray-900 mb-1">{item.name}</h3>
              <p className="text-gray-500 text-sm flex-1 mb-4">{item.desc}</p>
              <div className="flex items-center justify-between">
                <span className="font-black text-red-600 text-lg">{fmt(item.price)}</span>
                <button onClick={() => addToCart(item)}
                  className="px-4 py-2 rounded-xl text-xs font-black text-white transition-all hover:scale-105 active:scale-95"
                  style={{ background: "#C0392B" }}>
                  + Add
                </button>
              </div>
            </div>
          ))}
        </div>

        {/* WhatsApp order fallback */}
        <div className="mt-12 p-6 rounded-3xl text-center" style={{ background: "#1a0a00" }}>
          <p className="text-2xl mb-2">💬</p>
          <h3 className="text-white font-bold mb-1">Prefer to order via WhatsApp?</h3>
          <p className="text-white/60 text-sm mb-4">Send us a message and we'll handle your order manually.</p>
          <a href={BRAND.whatsapp} target="_blank" rel="noreferrer"
            className="inline-block px-8 py-3 rounded-2xl font-bold text-white text-sm transition-all hover:scale-105"
            style={{ background: "#25D366" }}>
            💬 Order on WhatsApp
          </a>
        </div>
      </div>
    </div>
  );
}

// ─── CHECKOUT PAGE ───────────────────────────────────────────────────────────
function CheckoutPage({ cart, user, setCart, setPage }) {
  const [mode, setMode] = useState("pickup"); // pickup | delivery
  const [zone, setZone] = useState(null);
  const [form, setForm] = useState({ name: user?.isGuest ? "" : user?.name || "", phone: "", address: "", area: "", notes: "" });
  const [submitted, setSubmitted] = useState(false);

  const subtotal = cart.reduce((s, i) => s + i.price * i.qty, 0);
  const deliveryFee = mode === "delivery" && zone ? DELIVERY_ZONES[zone - 1].fee : 0;
  const total = subtotal + deliveryFee;

  const handleSubmit = (e) => {
    e.preventDefault();
    setSubmitted(true);
  };

  if (submitted) {
    return (
      <div className="pt-28 pb-16 min-h-screen bg-gray-50 flex items-center justify-center px-4">
        <div className="bg-white rounded-3xl shadow-xl p-8 max-w-sm w-full text-center">
          <div className="text-6xl mb-4">🎉</div>
          <h2 className="text-2xl font-black text-gray-900 mb-2">Order Placed!</h2>
          <p className="text-gray-500 mb-2">Your order has been received. We'll contact you shortly on <strong>{form.phone || "your number"}</strong>.</p>
          <p className="text-gray-400 text-sm mb-6">Or follow up on WhatsApp 👇</p>
          <a href={BRAND.whatsapp} target="_blank" rel="noreferrer"
            className="block w-full py-3 rounded-2xl font-bold text-white mb-3"
            style={{ background: "#25D366" }}>
            💬 Chat on WhatsApp
          </a>
          <button onClick={() => { setCart([]); setPage("home"); }}
            className="w-full py-3 rounded-2xl font-bold text-red-600 border-2 border-red-200">
            Back to Home
          </button>
        </div>
      </div>
    );
  }

  return (
    <div className="pt-24 pb-16 min-h-screen bg-gray-50">
      <div className="max-w-2xl mx-auto px-4">
        <h1 className="text-3xl font-black text-gray-900 mb-2" style={{ fontFamily: "Georgia, serif" }}>Checkout</h1>
        <p className="text-gray-500 mb-8">Review your order and choose how you'd like to receive it.</p>

        {/* Order summary */}
        <div className="bg-white rounded-2xl shadow-sm p-5 mb-5">
          <h3 className="font-bold text-gray-800 mb-3">Order Summary</h3>
          {cart.map(item => (
            <div key={item.id} className="flex justify-between items-center py-2 border-b border-gray-50 last:border-0">
              <span className="text-sm text-gray-700">{item.emoji} {item.name} × {item.qty}</span>
              <span className="text-sm font-semibold text-gray-800">{fmt(item.price * item.qty)}</span>
            </div>
          ))}
          <div className="flex justify-between mt-3 font-semibold text-gray-700">
            <span>Subtotal</span><span>{fmt(subtotal)}</span>
          </div>
        </div>

        {/* Pickup / Delivery toggle */}
        <div className="bg-white rounded-2xl shadow-sm p-5 mb-5">
          <h3 className="font-bold text-gray-800 mb-3">Receiving Method</h3>
          <div className="grid grid-cols-2 gap-3">
            {["pickup", "delivery"].map(m => (
              <button key={m} onClick={() => setMode(m)}
                className={`py-3 rounded-xl font-bold text-sm capitalize transition-all ${mode === m ? "text-white" : "bg-gray-100 text-gray-600 hover:bg-gray-200"}`}
                style={mode === m ? { background: "#C0392B" } : {}}>
                {m === "pickup" ? "🏪 Pickup" : "🛵 Delivery"}
              </button>
            ))}
          </div>
        </div>

        {/* Delivery zone */}
        {mode === "delivery" && (
          <div className="bg-white rounded-2xl shadow-sm p-5 mb-5">
            <h3 className="font-bold text-gray-800 mb-1">Delivery Zone</h3>
            <p className="text-xs text-gray-400 mb-3">Delivery charges may vary depending on your area.</p>
            <div className="space-y-2">
              {DELIVERY_ZONES.map(z => (
                <button key={z.zone} onClick={() => setZone(z.zone)}
                  className={`w-full flex justify-between items-center p-3 rounded-xl border-2 text-left transition-all ${zone === z.zone ? "border-red-500 bg-red-50" : "border-gray-100 hover:border-gray-200"}`}>
                  <div>
                    <p className="font-bold text-sm text-gray-800">{z.label}</p>
                    <p className="text-xs text-gray-500">{z.areas}</p>
                  </div>
                  <span className={`font-black text-sm ${zone === z.zone ? "text-red-600" : "text-gray-700"}`}>{fmt(z.fee)}</span>
                </button>
              ))}
            </div>
          </div>
        )}

        {/* Contact form */}
        <form onSubmit={handleSubmit} className="bg-white rounded-2xl shadow-sm p-5 mb-5 space-y-3">
          <h3 className="font-bold text-gray-800 mb-1">Your Details</h3>
          <input required placeholder="Full Name" value={form.name}
            onChange={e => setForm({ ...form, name: e.target.value })}
            className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
          <input required placeholder="Phone Number" value={form.phone}
            onChange={e => setForm({ ...form, phone: e.target.value })}
            className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
          {mode === "delivery" && (
            <>
              <input required placeholder="Delivery Address" value={form.address}
                onChange={e => setForm({ ...form, address: e.target.value })}
                className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
              <input placeholder="Nearest Landmark / Area" value={form.area}
                onChange={e => setForm({ ...form, area: e.target.value })}
                className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400" />
            </>
          )}
          <textarea placeholder="Order notes (optional)" value={form.notes}
            onChange={e => setForm({ ...form, notes: e.target.value })}
            rows={2}
            className="w-full border border-gray-200 rounded-xl px-4 py-3 text-sm focus:outline-none focus:border-red-400 resize-none" />

          {/* Total */}
          <div className="pt-3 border-t">
            {mode === "delivery" && zone && (
              <div className="flex justify-between text-sm text-gray-600 mb-1">
                <span>Delivery Fee</span><span>{fmt(deliveryFee)}</span>
              </div>
            )}
            <div className="flex justify-between font-black text-lg text-gray-900 mb-4">
              <span>Total</span><span style={{ color: "#C0392B" }}>{fmt(total)}</span>
            </div>
            <button type="submit"
              disabled={mode === "delivery" && !zone}
              className="w-full py-4 rounded-2xl font-black text-white text-sm tracking-wide transition-all hover:scale-[1.02] active:scale-95 disabled:opacity-50 disabled:cursor-not-allowed"
              style={{ background: "linear-gradient(90deg,#C0392B,#E74C3C)" }}>
              Place Order — {fmt(total)} →
            </button>
            <p className="text-center text-xs text-gray-400 mt-2">Payment collected on delivery/pickup</p>
          </div>
        </form>
      </div>
    </div>
  );
}

// ─── LOCATIONS PAGE ───────────────────────────────────────────────────────────
function LocationsPage() {
  return (
    <div className="pt-24 pb-16 min-h-screen bg-gray-50">
      <div className="max-w-6xl mx-auto px-4">
        <div className="text-center py-10">
          <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Find Us</span>
          <h1 className="text-4xl font-black text-gray-900 mt-2 mb-3" style={{ fontFamily: "Georgia, serif" }}>
            Our Locations
          </h1>
          <p className="text-gray-500">4 branches across Freetown, Sierra Leone 🇸🇱</p>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          {LOCATIONS.map(loc => (
            <div key={loc.id} className="bg-white rounded-3xl shadow-sm overflow-hidden hover:shadow-lg transition-shadow">
              {/* Map placeholder */}
              <div className="h-40 flex items-center justify-center relative overflow-hidden"
                style={{ background: "linear-gradient(135deg, #1a0a00 0%, #3d1a00 100%)" }}>
                <div className="absolute inset-0 opacity-10"
                  style={{ backgroundImage: "radial-gradient(circle at 30% 50%, #F39C12 0%, transparent 60%), radial-gradient(circle at 70% 50%, #E74C3C 0%, transparent 60%)" }} />
                <div className="text-center z-10">
                  <div className="text-5xl mb-1">📍</div>
                  <span className="text-white/60 text-xs">Zone {loc.zone} — {DELIVERY_ZONES[loc.zone - 1].label.split("—")[1].trim()}</span>
                </div>
              </div>

              <div className="p-5">
                <h3 className="font-black text-gray-900 text-lg mb-1">{loc.name}</h3>
                <p className="text-gray-500 text-sm mb-1">📍 {loc.address}</p>
                <p className="text-gray-500 text-sm mb-1">🕒 {loc.hours}</p>
                <p className="text-gray-500 text-sm mb-4">📞 {loc.phone}</p>
                <div className="flex gap-2">
                  <a href={`tel:${loc.phone}`}
                    className="flex-1 py-2 rounded-xl text-sm font-bold text-center text-white transition-all hover:scale-105"
                    style={{ background: "#C0392B" }}>
                    📞 Call
                  </a>
                  <a href={BRAND.whatsapp} target="_blank" rel="noreferrer"
                    className="flex-1 py-2 rounded-xl text-sm font-bold text-center text-white transition-all hover:scale-105"
                    style={{ background: "#25D366" }}>
                    💬 WhatsApp
                  </a>
                  <a href={`https://maps.google.com/?q=${encodeURIComponent(loc.address)}`} target="_blank" rel="noreferrer"
                    className="flex-1 py-2 rounded-xl text-sm font-bold text-center border-2 border-gray-200 text-gray-600 hover:bg-gray-50 transition-all">
                    🗺️ Map
                  </a>
                </div>
              </div>
            </div>
          ))}
        </div>

        {/* Delivery zones info */}
        <div className="mt-12 bg-white rounded-3xl shadow-sm p-6">
          <h2 className="font-black text-gray-900 text-xl mb-2">🛵 Delivery Zones</h2>
          <p className="text-gray-500 text-sm mb-5">Delivery charges may vary depending on your area.</p>
          <div className="space-y-3">
            {DELIVERY_ZONES.map(z => (
              <div key={z.zone} className="flex items-center justify-between p-4 rounded-2xl"
                style={{ background: "#f9f9f9" }}>
                <div>
                  <p className="font-bold text-gray-800 text-sm">{z.label}</p>
                  <p className="text-gray-500 text-xs">{z.areas}</p>
                </div>
                <span className="font-black text-red-600">{fmt(z.fee)}</span>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
}

// ─── ABOUT PAGE ───────────────────────────────────────────────────────────────
function AboutPage() {
  return (
    <div className="pt-20 pb-16 min-h-screen">
      {/* Hero */}
      <section className="py-20 px-4 text-center" style={{ background: "linear-gradient(135deg,#1a0a00,#3d0e00)" }}>
        <span className="text-xs font-bold tracking-widest text-yellow-400 uppercase">Our Story</span>
        <h1 className="text-4xl font-black text-white mt-3 mb-4" style={{ fontFamily: "Georgia, serif" }}>
          Born in Freetown. <br />Built for You.
        </h1>
        <p className="text-white/70 max-w-xl mx-auto">
          Chicken Town started as a dream to bring Freetown its own premium fast-food brand — one that understands local taste, celebrates West African flavour, and serves it with global standards.
        </p>
      </section>

      {/* Story */}
      <section className="py-16 px-4 bg-white">
        <div className="max-w-3xl mx-auto">
          <div className="grid grid-cols-1 md:grid-cols-2 gap-10 items-center">
            <div>
              <h2 className="text-2xl font-black text-gray-900 mb-4" style={{ fontFamily: "Georgia, serif" }}>
                Where It All Started
              </h2>
              <p className="text-gray-600 mb-3 leading-relaxed">
                Founded in 2020, Chicken Town opened its first branch on Wilberforce Street with one goal: serve the crispiest, most flavourful chicken in Sierra Leone. We use locally sourced ingredients where possible, prepared fresh each morning.
              </p>
              <p className="text-gray-600 leading-relaxed">
                Today, we operate 4 branches across Freetown and serve thousands of satisfied customers every week — from quick lunch breaks to family weekend feasts.
              </p>
            </div>
            <div className="rounded-3xl overflow-hidden flex items-center justify-center h-56"
              style={{ background: "linear-gradient(135deg,#C0392B,#F39C12)" }}>
              <div className="text-center text-white">
                <div className="text-7xl mb-2">🍗</div>
                <p className="font-black text-xl">Est. 2020</p>
                <p className="text-white/70 text-sm">Freetown, Sierra Leone</p>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* Values */}
      <section className="py-16 px-4 bg-gray-50">
        <div className="max-w-6xl mx-auto">
          <div className="text-center mb-10">
            <h2 className="text-3xl font-black text-gray-900" style={{ fontFamily: "Georgia, serif" }}>What We Stand For</h2>
          </div>
          <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {[
              { icon: "🌿", title: "Freshness First", desc: "We prepare ingredients fresh daily. No pre-cooked batches sitting under heat lamps." },
              { icon: "🤝", title: "Community Roots", desc: "We're proud to be a Sierra Leonean brand. We hire locally, source locally, and give back locally." },
              { icon: "⭐", title: "Quality Always", desc: "From our spice blend to our packaging, every detail is thought through with care." },
            ].map(v => (
              <div key={v.title} className="bg-white rounded-2xl p-6 shadow-sm">
                <div className="text-4xl mb-3">{v.icon}</div>
                <h3 className="font-black text-gray-900 mb-2">{v.title}</h3>
                <p className="text-gray-500 text-sm">{v.desc}</p>
              </div>
            ))}
          </div>
        </div>
      </section>

      {/* FAQ */}
      <section className="py-16 px-4 bg-white">
        <div className="max-w-2xl mx-auto">
          <div className="text-center mb-10">
            <span className="text-xs font-bold tracking-widest text-red-600 uppercase">FAQs</span>
            <h2 className="text-3xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>Frequently Asked</h2>
          </div>
          <div className="space-y-3">
            {FAQS.map((faq, i) => (
              <FAQItem key={i} faq={faq} />
            ))}
          </div>
        </div>
      </section>
    </div>
  );
}

function FAQItem({ faq }) {
  const [open, setOpen] = useState(false);
  return (
    <div className="border border-gray-100 rounded-2xl overflow-hidden">
      <button onClick={() => setOpen(!open)}
        className="w-full text-left p-4 flex justify-between items-center hover:bg-gray-50 transition-colors">
        <span className="font-semibold text-gray-800 text-sm pr-4">{faq.q}</span>
        <span className={`text-gray-400 flex-shrink-0 transition-transform ${open ? "rotate-180" : ""}`}>▼</span>
      </button>
      {open && (
        <div className="px-4 pb-4 text-sm text-gray-600 border-t border-gray-50 pt-3">
          {faq.a}
        </div>
      )}
    </div>
  );
}

// ─── CONTACT PAGE ─────────────────────────────────────────────────────────────
function ContactPage() {
  return (
    <div className="pt-24 pb-16 min-h-screen bg-gray-50">
      <div className="max-w-4xl mx-auto px-4">
        <div className="text-center py-10">
          <span className="text-xs font-bold tracking-widest text-red-600 uppercase">Get In Touch</span>
          <h1 className="text-4xl font-black text-gray-900 mt-2" style={{ fontFamily: "Georgia, serif" }}>Contact Us</h1>
          <p className="text-gray-500 mt-2">We'd love to hear from you — reach us through any of these channels.</p>
        </div>

        <div className="grid grid-cols-1 md:grid-cols-2 gap-6 mb-8">
          {/* Quick contact */}
          <div className="bg-white rounded-3xl shadow-sm p-6 space-y-4">
            <h3 className="font-black text-gray-900 text-lg mb-2">Quick Contact</h3>
            {[
              { icon: "📞", label: "Call Us", value: BRAND.phone, href: `tel:${BRAND.phone}` },
              { icon: "📧", label: "Email", value: BRAND.email, href: `mailto:${BRAND.email}` },
              { icon: "💬", label: "WhatsApp", value: "Chat with us now", href: BRAND.whatsapp },
            ].map(c => (
              <a key={c.label} href={c.href} target="_blank" rel="noreferrer"
                className="flex items-center gap-4 p-3 rounded-2xl hover:bg-gray-50 transition-colors">
                <span className="text-2xl w-10 h-10 flex items-center justify-center rounded-xl bg-gray-100">{c.icon}</span>
                <div>
                  <p className="text-xs text-gray-500">{c.label}</p>
                  <p className="font-semibold text-gray-800 text-sm">{c.value}</p>
                </div>
              </a>
            ))}
          </div>

          {/* Social media */}
          <div className="bg-white rounded-3xl shadow-sm p-6">
            <h3 className="font-black text-gray-900 text-lg mb-4">Follow Us</h3>
            <div className="space-y-3">
              {[
                { icon: "f", name: "Facebook", handle: "@ChickenTownSL", color: "#1877F2", href: "#" },
                { icon: "▶", name: "Instagram", handle: "@chickentownsl", color: "#E1306C", href: "#" },
                { icon: "♪", name: "TikTok", handle: "@chickentownsl", color: "#000000", href: "#" },
                { icon: "✉", name: "WhatsApp", handle: "Chat & Order", color: "#25D366", href: BRAND.whatsapp },
              ].map(s => (
                <a key={s.name} href={s.href} target="_blank" rel="noreferrer"
                  className="flex items-center gap-3 p-3 rounded-2xl hover:bg-gray-50 transition-colors">
                  <div className="w-10 h-10 rounded-full flex items-center justify-center text-white text-sm font-bold flex-shrink-0"
                    style={{ background: s.color }}>
                    {s.icon}
                  </div>
                  <div>
                    <p className="font-bold text-gray-800 text-sm">{s.name}</p>
                    <p className="text-gray-500 text-xs">{s.handle}</p>
                  </div>
                </a>
              ))}
            </div>
          </div>
        </div>

        {/* Newsletter */}
        <div className="rounded-3xl p-8 text-center"
          style={{ background: "linear-gradient(135deg,#1a0a00,#3d0e00)" }}>
          <h3 className="text-white font-black text-xl mb-2">Stay in the Loop 🔔</h3>
          <p className="text-white/60 text-sm mb-5">Get deals, new menu updates, and offers before anyone else.</p>
          <div className="flex gap-2 max-w-sm mx-auto">
            <input type="email" placeholder="Your email address"
              className="flex-1 rounded-xl px-4 py-3 text-sm focus:outline-none" />
            <button className="px-5 py-3 rounded-xl font-bold text-sm text-white transition-all hover:scale-105"
              style={{ background: "#C0392B" }}>
              Subscribe
            </button>
          </div>
        </div>
      </div>
    </div>
  );
}

// ─── FOOTER ───────────────────────────────────────────────────────────────────
function Footer({ setPage }) {
  return (
    <footer style={{ background: "#0d0600" }} className="text-white/60 py-12 px-4">
      <div className="max-w-6xl mx-auto">
        <div className="grid grid-cols-2 md:grid-cols-4 gap-8 mb-10">
          <div className="col-span-2 md:col-span-1">
            <div className="flex items-center gap-2 mb-3">
              <span className="text-2xl">🍗</span>
              <span className="text-white font-black" style={{ fontFamily: "Georgia, serif" }}>CHICKEN TOWN</span>
            </div>
            <p className="text-xs leading-relaxed mb-4">Freetown's favourite crispy chicken. Fresh daily, served with pride.</p>
            <SocialBar />
          </div>

          <div>
            <h4 className="text-white font-bold text-sm mb-3">Quick Links</h4>
            <div className="space-y-2">
              {["home", "menu", "locations", "about", "contact"].map(p => (
                <button key={p} onClick={() => setPage(p)}
                  className="block text-xs capitalize hover:text-white transition-colors">{p}</button>
              ))}
            </div>
          </div>

          <div>
            <h4 className="text-white font-bold text-sm mb-3">Locations</h4>
            <div className="space-y-2">
              {LOCATIONS.map(l => (
                <p key={l.id} className="text-xs">{l.name.replace("Chicken Town — ", "")}</p>
              ))}
            </div>
          </div>

          <div>
            <h4 className="text-white font-bold text-sm mb-3">Contact</h4>
            <div className="space-y-2 text-xs">
              <p>📞 {BRAND.phone}</p>
              <p>📧 {BRAND.email}</p>
              <a href={BRAND.whatsapp} target="_blank" rel="noreferrer" className="block hover:text-white">💬 WhatsApp Us</a>
            </div>
          </div>
        </div>

        <div className="border-t border-white/10 pt-6 flex flex-col md:flex-row items-center justify-between gap-3 text-xs">
          <p>© {new Date().getFullYear()} Chicken Town. All rights reserved. Freetown, Sierra Leone 🇸🇱</p>
          <p>Made with ❤️ for Freetown</p>
        </div>
      </div>
    </footer>
  );
}

// ─── APP ROOT ─────────────────────────────────────────────────────────────────
export default function App() {
  const [splashDone, setSplashDone] = useState(false);
  const [user, setUser] = useState(null);
  const [page, setPage] = useState("home");
  const [cart, setCart] = useState([]);
  const [showCart, setShowCart] = useState(false);

  const addToCart = (item) => {
    setCart(prev => {
      const existing = prev.find(i => i.id === item.id);
      if (existing) return prev.map(i => i.id === item.id ? { ...i, qty: i.qty + 1 } : i);
      return [...prev, { ...item, qty: 1 }];
    });
  };

  const cartCount = cart.reduce((s, i) => s + i.qty, 0);

  const pageProps = { setPage, cart, setCart, user, addToCart };

  if (!splashDone) return <Splash onDone={() => setSplashDone(true)} />;
  if (!user) return <AuthModal onAuth={(u) => setUser(u)} />;

  return (
    <div className="min-h-screen bg-white font-sans">
      <Navbar user={user} onLogout={() => setUser(null)} cartCount={cartCount}
        setPage={setPage} page={page} setShowCart={setShowCart} />

      {showCart && <CartDrawer cart={cart} setCart={setCart} onClose={() => setShowCart(false)} setPage={setPage} />}

      <main>
        {page === "home" && <HomePage {...pageProps} />}
        {page === "menu" && <MenuPage {...pageProps} />}
        {page === "checkout" && <CheckoutPage {...pageProps} />}
        {page === "locations" && <LocationsPage />}
        {page === "about" && <AboutPage />}
        {page === "contact" && <ContactPage />}
      </main>

      {page !== "checkout" && <Footer setPage={setPage} />}
    </div>
  );
}

