# 🎥 POV Faceless Channel Domination

✨ **First-Person POV Image & Video Prompt Generator** ✨

Transform **any short description** into a **hyper-realistic cinematic POV prompt** ready for AI tools like:

- 🖼️ **Flux (black-forest-labs/flux-1.1-pro-ultra-finetuned)**
- 🎬 **Kling (kwaivgi/kling-v1.6-pro)**
- 🖌️ **Stable Diffusion / MidJourney**
- 📽️ **Runway Gen-3 Alpha / Pika Labs**

---

## ⚡ Features

✅ Converts a short **user input** into a **single immersive POV prompt**
✅ Optimized for **text-to-image** & **text-to-video** AI models
✅ Includes **visible limbs** for realism & immersion
✅ Rich **sensory details**: textures, lighting, sound, smell
✅ **Structured formatting** for AI consistency
✅ Output is **always under 950 characters**

---

## 🛠️ How It Works

1. 🔹 User provides a **short description** (e.g., `"POV: You’re a Viking at Sea"`)
2. 🔹 Generator transforms it into a **cinematic, AI-ready prompt**
3. 🔹 Output JSON format:

```json
{
  "prompt": "First-person view POV GoPro shot of my calloused hands gripping the rough wooden oar, veins straining as I pull through the churning icy waters... (continues under 950 chars)"
}
```

---

## 📌 Example Inputs & Outputs

### 🛡️ Input:

```txt
POV: You’re a Knight in Battle
```

### 🎬 Output:

```json
{
  "prompt": "First-person view POV GoPro shot of my gauntleted hands gripping the hilt of a longsword, the steel gleaming under the afternoon sun. Blood and mud splatter my armor as I brace for the enemy’s charge... (continues under 950 chars)"
}
```

---

## 🌍 API Usage

### 🔗 Replicate Endpoint

```http
POST https://api.replicate.com/v1/predictions/{{ $json["id"] }}
```

### 🧩 Example Call

```bash
curl -X POST "https://api.replicate.com/v1/predictions/{{ $json['id'] }}" \
  -H "Authorization: Token $REPLICATE_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
        "version": "black-forest-labs/flux-1.1-pro-ultra-finetuned",
        "input": {
            "prompt": "POV: You’re a Viking at Sea"
        }
      }'
```

---

## 📜 POV Rules & Guidelines

✔️ **First-person only** (GoPro-style immersion)
✔️ **Visible limbs** interacting naturally
✔️ **Interactive environment** (gripping, touching, moving)
✔️ **Sensory detail** (sight, touch, sound, smell, weather)
✔️ **Structured output** → Foreground → Background

---

## 🚀 Perfect For

- 📺 **Faceless YouTube Channels**
- 🎮 **Gaming POV Trailers**
- 🎥 **Cinematic AI Short Films**
- 📸 **Hyper-realistic AI Thumbnails**
