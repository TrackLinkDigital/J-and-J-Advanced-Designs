/**
 * J&J Applied Designs — Square Checkout Worker
 * ------------------------------------------------
 * SECURITY MODEL: the browser NEVER sends a price. It sends only a
 * product id (+ variant, for items that have one). Every price is
 * looked up from CATALOG below, which lives only on the server.
 * This means editing the page's JS or intercepting the request can't
 * change what a customer is charged.
 *
 * When you add/remove/reprice a product, edit CATALOG here and
 * redeploy the Worker — that is the ONLY place prices should ever
 * be defined for checkout purposes. (Keep index.html's display
 * prices in sync with this file.)
 *
 * REQUIRED Cloudflare Worker environment variables (set in dashboard,
 * NOT in this file):
 *   SQUARE_ACCESS_TOKEN   - your Sandbox or Production access token
 *   SQUARE_LOCATION_ID    - your Sandbox or Production location id
 *   SQUARE_ENV            - exactly "production" for real sales; anything
 *                           else uses the Square sandbox
 *   ALLOWED_ORIGIN        - origin only (no path, no trailing slash),
 *                           e.g. https://tracklinkdigital.github.io
 *   REDIRECT_URL          - full page customers return to after paying,
 *                           e.g. https://tracklinkdigital.github.io/J-and-J-Advanced-Designs/
 */
 
// ---------------------------------------------------------------
// PRICE CATALOG — all prices in whole dollars, converted to cents
// below.
//   variants  — cart must specify variant: "single" | "multi"
//   sized     — cart must specify size: "small"|"large" AND
//               variant: "single"|"multi" (4 price points each)
//   simple    — fixed price, no variant/size needed
//   bundles   — fixed price, no variant/size needed
// ---------------------------------------------------------------
const CATALOG = {
  variants: {
    "slitherstrike":              { name: "SlitherStrike (Articulated Snake)", single: 12.00, multi: 16.00 },
    "shadowthorn-dragon":         { name: "ShadowThorn Dragon",                single: 18.00, multi: 22.00 },
    "prismscale-dragon":          { name: "PrismScale Dragon",                 single: 18.00, multi: 22.00 },
    "shadowfang-keychain":        { name: "ShadowFang Dragon Keychain",        single: 7.99,  multi: 10.99 },
    "tiny-chomp-keychain":        { name: "Tiny Chomp T-Rex Keychain",         single: 5.00,  multi: 8.99  },
    "guardian-dragon-lamp":       { name: "Guardian Dragon Lamp",              single: 32.99, multi: 44.99 },
    "shellshift-turtle":          { name: "ShellShift Turtle",                 single: 10.00, multi: 15.00 },
    "scaleshift-egg":             { name: "ScaleShift Dragon Egg",             single: 12.99, multi: 15.00 },
    "pikapause-dock":             { name: "PikaPause Controller Dock",         single: 34.99, multi: 45.00 },
    "hexarack":                   { name: "HexaRack Gaming Organizer",         single: 59.99, multi: 74.99 },
    "gyrosphere-spinner":         { name: "GyroSphere Spinner",                single: 5.99,  multi: 8.00  },
    "cosmic-star-wand":           { name: "Cosmic Star Wand (Large)",          single: 10.00, multi: 14.00 },
    "retrovault-case":            { name: "RetroVault Switch Game Card Case",  single: 16.00, multi: 20.00 },
    "dreamglow-fairy-lamp":       { name: "DreamGlow Fairy Lamp",              single: 24.99, multi: 29.99 },
    "auratwist-lamp":             { name: "AuraTwist LED Lamp",                single: 24.99, multi: 29.99 },
    "octospin-ring":              { name: "Octospin Spinner Ring",             single: 5.00,  multi: 8.00  },
    "infinity-helix-wand":        { name: "Infinity Helix Wand",               single: 14.99, multi: 18.99 },
    "infinity-helixlink":         { name: "Infinity HelixLink",                single: 12.99, multi: 15.00 },
    "infinity-twist-passthrough": { name: "Infinity Twist Passthrough",        single: 12.99, multi: 16.99 },
    "infinity-cubeshift":         { name: "Infinity CubeShift",                single: 9.99,  multi: 16.99 },
    "hyper-wheel":                { name: "Hyper Wheel",                       single: 14.99, multi: 17.99 },
    "clickstack":                 { name: "ClickStack",                        single: 8.99,  multi: 11.99 },
    "magtrick-flipboard":         { name: "MagTrick FlipBoard",                single: 10.99, multi: 14.99 },
    "skyfang":                    { name: "SkyFang",                           single: 12.99, multi: 16.99 },
    "stormwing":                  { name: "StormWing",                         single: 12.99, multi: 16.99 },
    "snapjaw-shark":              { name: "SnapJaw Shark",                     single: 8.99,  multi: 13.99 },
    "paint-pop-lamp":             { name: "Paint Pop Lamp",                    single: 19.99, multi: 25.99 },
    "mindscape-lamp":             { name: "MindScape Lamp",                    single: 39.99, multi: 54.99 },
    "shadowflame-dragon":         { name: "ShadowFlame Dragon",                single: 18.00, multi: 22.00 },
    "stormscale-dragon":          { name: "StormScale Dragon",                 single: 18.00, multi: 22.00 },
    "venomspine-dragon":          { name: "VenomSpine Dragon",                 single: 18.00, multi: 22.00 },
    "inferno-dragon":             { name: "Inferno Dragon",                    single: 18.00, multi: 22.00 },
    "twisty-bao":                 { name: "Twisty Bao",                        single: 10.00, multi: 13.99 },
    "zenclick":                   { name: "ZenClick",                          single: 12.99, multi: 15.99 },
    // PRICE NOT CONFIRMED BY CUSTOMER — same placeholder as index.html.
    // Update both this entry AND index.html together if price changes,
    // or checkout will charge the wrong amount.
    "mystical-unicorn-dragon":    { name: "Mystical Unicorn Dragon",           single: 19.99, multi: 24.99 },
    // Flat $10 regardless of variant — front-end never sends "multi" for this
    // item (noMulti:true), but multi is set to match single as a safe fallback.
    "pencil-pen":                 { name: "Pencil Pen",                        single: 10.00, multi: 10.00 },
  },
  sized: {
    "sensory-wiggle-ray": { name: "Sensory Wiggle Ray",     small: { single: 9.99, multi: 14.99 }, large: { single: 15.00, multi: 20.99 } },
    "orbitcore-fidget":   { name: "OrbitCore Gear Fidget",  small: { single: 4.99, multi: 8.99  }, large: { single: 8.99,  multi: 12.99 } },
    "chompasaurus":       { name: "Chompasaurus",           small: { single: 7.99, multi: 10.99 }, large: { single: 11.99, multi: 14.99 } },
  },
  simple: {
    "whack-a-mole":       { name: "Whack-A-Mole",       price: 7.99 },
    "skyspin-launcher":   { name: "SkySpin Launcher",   price: 17.99 },
    "splat-dice-lamp":    { name: "Splat Dice Lamp",    price: 30.00 },
    "mystery-dragon-egg": { name: "Mystery Dragon Egg", price: 22.00 },
  },
  // 13.75" x 13.75" HueForge portrait prints — cart must specify
  // frame: "none" | "frame" | "led". Which specific design is
  // customer-picked and travels in item.note, not a separate catalog
  // entry — price doesn't change by design, only by frame option.
  framed: {
    "hueforge-portrait": { name: "HueForge Portrait", options: { none: 35.00, frame: 45.00, led: 60.00 } },
  },
  // 12" vinyl-record-sized prints — flat price, no frame tiers. Which
  // design is picked travels in item.note, same pattern as framed above.
  vinyl: {
    "vinyl-record-print": { name: "Vinyl Record Print", price: 25.00 },
  },
  bundles: {
    "dragon-collection":     { name: "Dragon Collection (pick 3 dragons)", price: 50.00 },
    "hatchling-collection":  { name: "Hatchling Collection",               price: 39.99 },
    "gaming-collection":     { name: "Gaming Collection",                  price: 86.99 },
    "ultimate-fidget-box":   { name: "Ultimate Fidget Collection",         price: 50.00 },
    "ocean-collection":      { name: "Ocean Collection",                   price: 30.00 },
    "wizard-collection":     { name: "Wizard Collection",                  price: 49.99 },
    "home-collection":       { name: "Home Collection",                    price: 89.99 },
    "pocket-collection":     { name: "Pocket Collection",                  price: 24.99 },
    "mystery-fidget-box":    { name: "Mystery Fidget Box",                 price: 19.99 },
    "mystery-dragon-box":    { name: "Mystery Dragon Box",                 price: 59.99 },
    "surprise-gamer-box":    { name: "Surprise Gamer Box",                 price: 69.99 },
    "premium-mystery-box":   { name: "Premium Mystery Box",                price: 95.99 },
  },
};
 
const MAX_CART_LINES = 50;
 
export default {
  async fetch(request, env, ctx) {
    const corsHeaders = {
      "Access-Control-Allow-Origin": env.ALLOWED_ORIGIN || "*",
      "Access-Control-Allow-Methods": "POST, GET, OPTIONS",
      "Access-Control-Allow-Headers": "Content-Type",
    };
 
    if (request.method === "OPTIONS") {
      return new Response(null, { headers: corsHeaders });
    }
 
    // ---- Reviews routes (added). Anything else falls through to checkout. ----
    const path = new URL(request.url).pathname.replace(/\/+$/, "") || "/";
    if (path === "/reviews" && request.method === "GET") return listApprovedReviews(env, corsHeaders);
    if (path === "/review" && request.method === "POST") return submitReview(request, env, ctx, corsHeaders);
    if (path === "/admin" && request.method === "GET") return adminPage();
    if (path.startsWith("/admin/api/")) return adminApi(request, env, path);

    if (request.method !== "POST") {
      return jsonError(corsHeaders, "Method not allowed", 405);
    }
 
    let body;
    try {
      body = await request.json();
    } catch (e) {
      return jsonError(corsHeaders, "Invalid JSON body", 400);
    }
 
    const cart = body.cart;
    if (!Array.isArray(cart) || cart.length === 0) {
      return jsonError(corsHeaders, "Cart is empty or missing", 400);
    }
    if (cart.length > MAX_CART_LINES) {
      return jsonError(corsHeaders, "Cart too large", 400);
    }
 
    // ---- Build line items using ONLY server-side catalog prices ----
    const lineItems = [];
    for (const item of cart) {
      const qty = Math.max(1, Math.min(50, parseInt(item.qty, 10) || 1));
      const id = String(item.id || "");
 
      if (CATALOG.variants[id]) {
        const product = CATALOG.variants[id];
        const variant = item.variant === "multi" ? "multi" : item.variant === "single" ? "single" : null;
        if (!variant) {
          return jsonError(corsHeaders, `Missing/invalid variant for "${id}"`, 400);
        }
        const price = product[variant];
        // Cap is 220: a 4-color silk-blend pick with finish runs ~138 chars
        // before any customer-typed custom name is appended.
        const note = sanitizeNote(item.note, 220);
        const variantLabel = variant === "multi" ? "Multi-Color/Custom" : "Single Color";
        lineItems.push({
          name: `${product.name} (${variantLabel})${note ? ` - ${note}` : ""}`,
          quantity: String(qty),
          base_price_money: { amount: Math.round(price * 100), currency: "USD" },
        });
      } else if (CATALOG.sized[id]) {
        const product = CATALOG.sized[id];
        const size = item.size === "large" ? "large" : item.size === "small" ? "small" : null;
        const variant = item.variant === "multi" ? "multi" : item.variant === "single" ? "single" : null;
        if (!size || !variant) {
          return jsonError(corsHeaders, `Missing/invalid size or variant for "${id}"`, 400);
        }
        const price = product[size][variant];
        const note = sanitizeNote(item.note, 220);
        const sizeLabel = size === "large" ? "Large" : "Small";
        const variantLabel = variant === "multi" ? "Multi-Color/Custom" : "Single Color";
        lineItems.push({
          name: `${product.name} (${sizeLabel}, ${variantLabel})${note ? ` - ${note}` : ""}`,
          quantity: String(qty),
          base_price_money: { amount: Math.round(price * 100), currency: "USD" },
        });
      } else if (CATALOG.simple[id]) {
        const product = CATALOG.simple[id];
        lineItems.push({
          name: product.name,
          quantity: String(qty),
          base_price_money: { amount: Math.round(product.price * 100), currency: "USD" },
        });
      } else if (CATALOG.framed[id]) {
        const product = CATALOG.framed[id];
        const frame = ["none", "frame", "led"].includes(item.variant) ? item.variant : null;
        if (!frame) {
          return jsonError(corsHeaders, `Missing/invalid frame option for "${id}"`, 400);
        }
        const price = product.options[frame];
        const frameLabel = frame === "led" ? "Framed + LED" : frame === "frame" ? "Framed" : "No Frame";
        const note = sanitizeNote(item.note, 60); // e.g. "Design Astronaut DJ"
        lineItems.push({
          name: `${product.name} (${frameLabel})${note ? ` - ${note}` : ""}`,
          quantity: String(qty),
          base_price_money: { amount: Math.round(price * 100), currency: "USD" },
        });
      } else if (CATALOG.vinyl[id]) {
        const product = CATALOG.vinyl[id];
        const note = sanitizeNote(item.note, 60); // e.g. "Design Spiral Portrait"
        lineItems.push({
          name: `${product.name}${note ? ` - ${note}` : ""}`,
          quantity: String(qty),
          base_price_money: { amount: Math.round(product.price * 100), currency: "USD" },
        });
      } else if (CATALOG.bundles[id]) {
        const bundle = CATALOG.bundles[id];
        const note = sanitizeNote(item.note, 450); // up to 4 colors + finish, per picked item, x3 items
        lineItems.push({
          name: `${bundle.name}${note ? ` - ${note}` : ""}`,
          quantity: String(qty),
          base_price_money: { amount: Math.round(bundle.price * 100), currency: "USD" },
        });
      } else {
        return jsonError(corsHeaders, `Unknown product id: "${id}"`, 400);
      }
    }
 
    const squareBase =
      env.SQUARE_ENV === "production"
        ? "https://connect.squareup.com"
        : "https://connect.squareupsandbox.com";
 
    const idempotencyKey = crypto.randomUUID();
 
    let squareResp, squareData;
    try {
      squareResp = await fetch(`${squareBase}/v2/online-checkout/payment-links`, {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          "Authorization": `Bearer ${env.SQUARE_ACCESS_TOKEN}`,
          "Square-Version": "2025-01-23",
        },
        body: JSON.stringify({
          idempotency_key: idempotencyKey,
          order: {
            location_id: env.SQUARE_LOCATION_ID,
            line_items: lineItems,
          },
          checkout_options: {
            // Full page URL (REDIRECT_URL), not the bare origin — the site
            // lives under a path on GitHub Pages.
            redirect_url: env.REDIRECT_URL || env.ALLOWED_ORIGIN || undefined,
            ask_for_shipping_address: true,
          },
        }),
      });
      squareData = await squareResp.json();
    } catch (err) {
      console.error("Square request failed:", err);
      return jsonError(corsHeaders, "Checkout is unavailable right now. Please try again or email us.", 502);
    }
 
    if (!squareResp.ok || !squareData.payment_link) {
      // Full detail stays in the Worker logs; the customer gets a generic message.
      console.error("Square API error:", squareData);
      return jsonError(corsHeaders, "Checkout is unavailable right now. Please try again or email us.", 502);
    }
 
    return new Response(JSON.stringify({ url: squareData.payment_link.url }), {
      headers: { ...corsHeaders, "Content-Type": "application/json" },
    });
  },
};
 
function jsonError(corsHeaders, message, status) {
  return new Response(JSON.stringify({ error: message }), {
    status,
    headers: { ...corsHeaders, "Content-Type": "application/json" },
  });
}
 
// Optional customer text (e.g. a name to add to a keychain). Keeps letters,
// numbers, spaces, accented Latin letters, and a few punctuation marks;
// strips everything else and caps length. This only ever affects display
// text on the order, never price.
function sanitizeNote(raw, maxLen = 40) {
  const str = typeof raw === "string" ? raw : "";
  return str.replace(/[^a-zA-Z0-9 .,'&\/()\-\u00C0-\u017F]/g, "").trim().slice(0, maxLen);
}
// =====================================================================
// REVIEWS (added) — stored in a Workers KV namespace bound as REVIEWS.
//
// Flow: customer submits -> saved as "pending" (never shown) -> you open
// https://<your-worker>/admin, sign in with ADMIN_TOKEN, and Approve or
// Delete. Approved reviews are served publicly at GET /reviews.
//
// Extra setup (see the notes that came with this file):
//   KV binding         REVIEWS       (Settings > Bindings > KV namespace)
//   Secret             ADMIN_TOKEN   (long random password for /admin)
//   Optional secrets   RESEND_API_KEY, NOTIFY_EMAIL, NOTIFY_FROM
//                      -> emails you when a new review arrives
// =====================================================================

const REVIEW_PRODUCTS = ["Custom order", "Ready-made item", "Fidget / desk toy", "Gaming gear", "Cosplay / armor", "Other"];
const MAX_REVIEW_TEXT = 1500;
const MAX_REVIEWS_PER_IP_PER_HOUR = 3;
const MAX_PUBLISHED = 500;

// true  = reviews go live immediately (you can delete any at /admin).
// false = reviews wait in your inbox until you press Approve at /admin.
// Reviews from customers who unticked "you may show my review" are never published automatically.
const AUTO_PUBLISH = true;

function jsonOk(headers, obj, status = 200) {
  return new Response(JSON.stringify(obj), {
    status,
    headers: { ...headers, "Content-Type": "application/json" },
  });
}

// Strips control characters (keeps tabs/newlines), trims, caps length.
function cleanText(raw, maxLen) {
  return (typeof raw === "string" ? raw : "")
    .replace(/[\u0000-\u0008\u000B\u000C\u000E-\u001F\u007F]/g, "")
    .trim()
    .slice(0, maxLen);
}

// "Sam Rivera" -> "Sam R."   (public pages never show full names)
function publicName(full) {
  const parts = full.split(/\s+/).filter(Boolean);
  if (parts.length < 2) return parts[0] || "Customer";
  return parts[0] + " " + parts[parts.length - 1][0].toUpperCase() + ".";
}

async function listApprovedReviews(env, corsHeaders) {
  if (!env.REVIEWS) return jsonOk(corsHeaders, { reviews: [] });
  const raw = await env.REVIEWS.get("approved");
  let reviews = [];
  try { reviews = raw ? JSON.parse(raw) : []; } catch (e) { reviews = []; }
  return jsonOk({ ...corsHeaders, "Cache-Control": "public, max-age=60" }, { reviews });
}

async function submitReview(request, env, ctx, corsHeaders) {
  if (!env.REVIEWS) return jsonError(corsHeaders, "Reviews are not set up yet.", 503);

  // Browsers always send Origin on cross-site posts; reject other sites.
  const origin = request.headers.get("Origin");
  if (env.ALLOWED_ORIGIN && origin && origin !== env.ALLOWED_ORIGIN) {
    return jsonError(corsHeaders, "Not allowed", 403);
  }

  let b;
  try { b = await request.json(); } catch (e) { return jsonError(corsHeaders, "Invalid JSON body", 400); }
  if (!b || typeof b !== "object") return jsonError(corsHeaders, "Invalid JSON body", 400);

  // Hidden spam-trap fields: real visitors leave these empty. Bots get a fake "ok".
  if (b._gotcha || b.botcheck) return jsonOk(corsHeaders, { ok: true });

  const rating = parseInt(b.rating, 10);
  const name = cleanText(b.name, 60);
  const email = cleanText(b.email, 120);
  const text = cleanText(b.review, MAX_REVIEW_TEXT);
  const product = REVIEW_PRODUCTS.includes(b.product) ? b.product : "";

  if (!(rating >= 1 && rating <= 5)) return jsonError(corsHeaders, "Please choose a star rating.", 400);
  if (!name) return jsonError(corsHeaders, "Please enter your name.", 400);
  if (!/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(email)) return jsonError(corsHeaders, "Please enter a valid email address.", 400);
  if (!text) return jsonError(corsHeaders, "Please write a few words about your experience.", 400);

  // Simple per-visitor limit so one person can't flood the inbox.
  const ip = request.headers.get("CF-Connecting-IP") || "unknown";
  const rlKey = "rl:" + ip;
  const used = parseInt(await env.REVIEWS.get(rlKey), 10) || 0;
  if (used >= MAX_REVIEWS_PER_IP_PER_HOUR) {
    return jsonError(corsHeaders, "Too many reviews from this connection. Please try again later.", 429);
  }
  await env.REVIEWS.put(rlKey, String(used + 1), { expirationTtl: 3600 });

  const now = new Date();
  const id = now.getTime() + "-" + crypto.randomUUID().slice(0, 8);
  const item = {
    id,
    name,
    email,
    rating,
    product,
    text,
    date: now.toISOString().slice(0, 10),
    okToDisplay: b.ok_to_display === true || b.ok_to_display === "yes",
  };
  const live = AUTO_PUBLISH && item.okToDisplay;
  if (live) {
    const rawA = await env.REVIEWS.get("approved");
    let approved = [];
    try { approved = rawA ? JSON.parse(rawA) : []; } catch (e) {}
    approved.unshift({ id: item.id, name: publicName(item.name), rating: item.rating, product: item.product, text: item.text, date: item.date });
    await env.REVIEWS.put("approved", JSON.stringify(approved.slice(0, MAX_PUBLISHED)));
  } else {
    await env.REVIEWS.put("pending:" + id, JSON.stringify(item));
  }

  ctx.waitUntil(notifyOwner(env, item, live));
  return jsonOk(corsHeaders, { ok: true });
}

// Optional: email you through Resend (free tier) when a review arrives.
async function notifyOwner(env, r, live) {
  if (!env.RESEND_API_KEY || !env.NOTIFY_EMAIL) return;
  try {
    await fetch("https://api.resend.com/emails", {
      method: "POST",
      headers: { "Authorization": "Bearer " + env.RESEND_API_KEY, "Content-Type": "application/json" },
      body: JSON.stringify({
        from: env.NOTIFY_FROM || "J&J Reviews <onboarding@resend.dev>",
        to: [env.NOTIFY_EMAIL],
        subject: "New review: " + r.rating + " stars from " + r.name,
        text: r.name + " (" + r.email + ")\n" + r.rating + "/5  " + r.product + "\n\n" + r.text +
              (live ? "\n\nThis review is already live on your site. Delete it on your Worker's /admin page if you don't want it."
                    : "\n\nThis review is waiting for you. Approve or delete it on your Worker's /admin page."),
      }),
    });
  } catch (e) {
    console.error("Review notification failed:", e);
  }
}

async function safeEqual(a, b) {
  const enc = new TextEncoder();
  const [ha, hb] = await Promise.all([
    crypto.subtle.digest("SHA-256", enc.encode(a)),
    crypto.subtle.digest("SHA-256", enc.encode(b)),
  ]);
  const x = new Uint8Array(ha), y = new Uint8Array(hb);
  let diff = 0;
  for (let i = 0; i < x.length; i++) diff |= x[i] ^ y[i];
  return diff === 0;
}

async function adminApi(request, env, path) {
  const h = { "Content-Type": "application/json", "Cache-Control": "no-store" };
  const reply = (obj, status = 200) => new Response(JSON.stringify(obj), { status, headers: h });

  if (!env.REVIEWS || !env.ADMIN_TOKEN) {
    return reply({ error: "Admin is not set up yet (needs the REVIEWS binding and ADMIN_TOKEN secret)." }, 503);
  }
  const auth = request.headers.get("Authorization") || "";
  if (!(await safeEqual(auth, "Bearer " + env.ADMIN_TOKEN))) {
    return reply({ error: "Wrong password." }, 401);
  }

  if (path === "/admin/api/list" && request.method === "GET") {
    const keys = (await env.REVIEWS.list({ prefix: "pending:" })).keys;
    const pending = [];
    for (const k of keys) {
      const raw = await env.REVIEWS.get(k.name);
      if (raw) { try { pending.push(JSON.parse(raw)); } catch (e) {} }
    }
    pending.sort((a, b) => (a.id < b.id ? 1 : -1));
    const rawA = await env.REVIEWS.get("approved");
    let approved = [];
    try { approved = rawA ? JSON.parse(rawA) : []; } catch (e) {}
    return reply({ pending, approved });
  }

  if (request.method !== "POST") return reply({ error: "Method not allowed" }, 405);
  let b;
  try { b = await request.json(); } catch (e) { return reply({ error: "Invalid JSON body" }, 400); }
  const id = String((b && b.id) || "");
  if (!id) return reply({ error: "Missing id" }, 400);

  if (path === "/admin/api/approve") {
    const raw = await env.REVIEWS.get("pending:" + id);
    if (!raw) return reply({ error: "That review was not found." }, 404);
    const r = JSON.parse(raw);
    if (!r.okToDisplay) return reply({ error: "This customer did not give permission to display their review." }, 400);
    const rawA = await env.REVIEWS.get("approved");
    let approved = [];
    try { approved = rawA ? JSON.parse(rawA) : []; } catch (e) {}
    approved.unshift({ id: r.id, name: publicName(r.name), rating: r.rating, product: r.product, text: r.text, date: r.date });
    await env.REVIEWS.put("approved", JSON.stringify(approved));
    await env.REVIEWS.delete("pending:" + id);
    return reply({ ok: true });
  }

  if (path === "/admin/api/delete") {
    if (b.from === "approved") {
      const rawA = await env.REVIEWS.get("approved");
      let approved = [];
      try { approved = rawA ? JSON.parse(rawA) : []; } catch (e) {}
      await env.REVIEWS.put("approved", JSON.stringify(approved.filter(x => x.id !== id)));
    } else {
      await env.REVIEWS.delete("pending:" + id);
    }
    return reply({ ok: true });
  }

  return reply({ error: "Not found" }, 404);
}

function adminPage() {
  return new Response(ADMIN_HTML, {
    headers: {
      "Content-Type": "text/html; charset=utf-8",
      "Cache-Control": "no-store",
      "X-Robots-Tag": "noindex, nofollow",
      "Content-Security-Policy":
        "default-src 'none'; style-src 'unsafe-inline'; script-src 'unsafe-inline'; connect-src 'self'; base-uri 'none'; form-action 'none'",
    },
  });
}

const ADMIN_HTML = `<!DOCTYPE html>
<html lang="en"><head><meta charset="UTF-8"><meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="robots" content="noindex"><title>Review inbox</title>
<style>
  body{margin:0;background:#f2f1ed;color:#1b1e24;font:16px/1.5 system-ui,sans-serif}
  header{background:#1b1e24;color:#fff;padding:16px 20px;border-bottom:6px solid #1f9d8a}
  header h1{margin:0;font-size:1.15rem}
  main{max-width:760px;margin:0 auto;padding:20px}
  h2{font-size:1.1rem;margin:28px 0 10px}
  .card{background:#fff;border:1px solid #dedad0;border-radius:10px;padding:16px;margin-bottom:12px}
  .top{display:flex;justify-content:space-between;gap:10px;flex-wrap:wrap;font-weight:600}
  .stars{color:#f0a93e;letter-spacing:2px}
  .meta{font-size:.82rem;color:#3a3f4b;margin:4px 0 8px}
  .text{white-space:pre-wrap;margin:0 0 12px}
  .warn{color:#c85a3f;font-size:.85rem;font-weight:600;margin-bottom:8px}
  button{font:600 .9rem system-ui,sans-serif;border:0;border-radius:8px;padding:9px 16px;cursor:pointer;margin-right:8px}
  .ok{background:#1f9d8a;color:#fff} .no{background:#fff;color:#c85a3f;border:1.5px solid #c85a3f}
  button:disabled{opacity:.5;cursor:not-allowed}
  input{font:inherit;padding:10px;border:1.5px solid #dedad0;border-radius:8px;width:100%;max-width:340px}
  .empty{color:#3a3f4b;font-style:italic}
  #err{color:#c85a3f;font-weight:600;margin:10px 0}
</style></head><body>
<header><h1>J&amp;J Applied Designs &mdash; Review inbox</h1></header>
<main>
  <div id="login">
    <p>Enter your admin password.</p>
    <input id="pw" type="password" autocomplete="current-password" placeholder="Admin password">
    <p><button class="ok" id="go">Sign in</button></p>
  </div>
  <div id="err" role="alert"></div>
  <div id="app" hidden>
    <h2>Waiting for your approval</h2><div id="pending"></div>
    <h2>Published on your site</h2><div id="approved"></div>
  </div>
</main>
<script>
var tok = '';
try { tok = sessionStorage.getItem('jjTok') || ''; } catch (e) {}
var errEl = document.getElementById('err');

function api(path, method, body) {
  return fetch('/admin/api/' + path, {
    method: method,
    headers: { 'Authorization': 'Bearer ' + tok, 'Content-Type': 'application/json' },
    body: body ? JSON.stringify(body) : undefined
  }).then(function (r) {
    return r.json().then(function (d) {
      if (!r.ok) throw new Error(d.error || ('Error ' + r.status));
      return d;
    });
  });
}
function el(tag, cls, text) {
  var e = document.createElement(tag);
  if (cls) e.className = cls;
  if (text != null) e.textContent = text;
  return e;
}
function stars(n) { return '\\u2605'.repeat(n) + '\\u2606'.repeat(5 - n); }

function card(r, isPending) {
  var c = el('div', 'card');
  var top = el('div', 'top');
  top.appendChild(el('span', '', r.name));
  top.appendChild(el('span', 'stars', stars(r.rating)));
  c.appendChild(top);
  var bits = [];
  if (isPending) bits.push(r.email);
  if (r.product) bits.push(r.product);
  if (r.date) bits.push(r.date);
  c.appendChild(el('div', 'meta', bits.join('  \\u00b7  ')));
  c.appendChild(el('p', 'text', r.text));
  if (isPending && !r.okToDisplay) {
    c.appendChild(el('div', 'warn', 'Customer did NOT give permission to display this review.'));
  }
  if (isPending) {
    var a = el('button', 'ok', 'Approve');
    a.disabled = !r.okToDisplay;
    a.onclick = function () { act('approve', { id: r.id }, a); };
    c.appendChild(a);
  }
  var d = el('button', 'no', 'Delete');
  d.onclick = function () {
    if (confirm('Delete this review for good?')) act('delete', { id: r.id, from: isPending ? 'pending' : 'approved' }, d);
  };
  c.appendChild(d);
  return c;
}
function fill(id, list, isPending, emptyText) {
  var box = document.getElementById(id);
  box.textContent = '';
  if (!list.length) { box.appendChild(el('p', 'empty', emptyText)); return; }
  list.forEach(function (r) { box.appendChild(card(r, isPending)); });
}
function load() {
  errEl.textContent = '';
  api('list', 'GET').then(function (d) {
    document.getElementById('login').hidden = true;
    document.getElementById('app').hidden = false;
    fill('pending', d.pending, true, 'Nothing waiting.');
    fill('approved', d.approved, false, 'No published reviews yet.');
  }).catch(function (e) {
    document.getElementById('app').hidden = true;
    document.getElementById('login').hidden = false;
    errEl.textContent = e.message;
  });
}
function act(what, body, btn) {
  btn.disabled = true;
  api(what, 'POST', body).then(load).catch(function (e) { errEl.textContent = e.message; btn.disabled = false; });
}
document.getElementById('go').onclick = function () {
  tok = document.getElementById('pw').value;
  try { sessionStorage.setItem('jjTok', tok); } catch (e) {}
  load();
};
document.getElementById('pw').onkeydown = function (e) { if (e.key === 'Enter') document.getElementById('go').click(); };
if (tok) load();
</script></body></html>`;
