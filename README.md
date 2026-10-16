<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>OurMoments - Interactive Birthday Surprise</title>
  
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  
  <!-- Font Awesome Icons -->
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
  
  <!-- Canvas Confetti Library -->
  <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
  
  <!-- Google Fonts -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Caveat:wght@600;700&family=Dancing+Script:wght@700&family=Inter:wght@300;400;500;600;700&family=Playfair+Display:ital,wght@0,600;0,800;1,400&display=swap" rel="stylesheet">

  <script>
    tailwind.config = {
      darkMode: 'class',
      theme: {
        extend: {
          colors: {
            brand: {
              50: '#fff1f2',
              100: '#ffe4e6',
              300: '#fda4af',
              500: '#f43f5e',
              600: '#e11d48',
              900: '#881337',
            },
            gold: {
              300: '#fde047',
              400: '#facc15',
              500: '#eab308',
            },
            midnight: '#0f172a',
            deepspace: '#090d16',
          },
          fontFamily: {
            sans: ['Inter', 'sans-serif'],
            serif: ['Playfair Display', 'serif'],
            handwriting: ['Caveat', 'cursive'],
            cursive: ['Dancing Script', 'cursive'],
          },
          animation: {
            'float': 'float 6s ease-in-out infinite',
            'float-slow': 'float 9s ease-in-out infinite',
            'pulse-glow': 'pulseGlow 2s cubic-bezier(0.4, 0, 0.6, 1) infinite',
            'twinkle': 'twinkle 3s ease-in-out infinite',
            'string-sway': 'stringSway 4s ease-in-out infinite',
          },
          keyframes: {
            float: {
              '0%, 100%': { transform: 'translateY(0px) rotate(0deg)' },
              '50%': { transform: 'translateY(-15px) rotate(3deg)' },
            },
            pulseGlow: {
              '0%, 100%': { opacity: 0.9, filter: 'drop-shadow(0 0 15px rgba(251, 191, 36, 0.8))' },
              '50%': { opacity: 0.4, filter: 'drop-shadow(0 0 4px rgba(251, 191, 36, 0.3))' },
            },
            twinkle: {
              '0%, 100%': { opacity: 0.3, transform: 'scale(0.8)' },
              '50%': { opacity: 1, transform: 'scale(1.2)' },
            },
            stringSway: {
              '0%, 100%': { transform: 'rotate(-1deg)' },
              '50%': { transform: 'rotate(1deg)' },
            }
          }
        }
      }
    }
  </script>

  <style>
    /* Custom Scrollbar & Aesthetics */
    ::-webkit-scrollbar {
      width: 6px;
      height: 6px;
    }
    ::-webkit-scrollbar-track {
      background: rgba(15, 23, 42, 0.6);
    }
    ::-webkit-scrollbar-thumb {
      background: rgba(244, 63, 94, 0.4);
      border-radius: 9999px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: rgba(244, 63, 94, 0.8);
    }
    
    /* Candle Flame Animation */
    .flame {
      transform-origin: center bottom;
      animation: flicker 0.1s ease-in-out infinite alternate;
    }
    @keyframes flicker {
      0% { transform: scale(1) rotate(-2deg); opacity: 0.95; }
      100% { transform: scale(1.1) rotate(2deg); opacity: 1; filter: drop-shadow(0 0 10px #f59e0b); }
    }

    /* Glassmorphism effects */
    .glass-card {
      background: rgba(30, 41, 59, 0.65);
      backdrop-filter: blur(16px);
      -webkit-backdrop-filter: blur(16px);
      border: 1px solid rgba(255, 255, 255, 0.12);
    }
    
    .glass-card-light {
      background: rgba(255, 255, 255, 0.85);
      backdrop-filter: blur(12px);
      border: 1px solid rgba(255, 255, 255, 0.3);
    }

    /* Envelope styling */
    .envelope-flap {
      clip-path: polygon(0 0, 50% 50%, 100% 0);
      transform-origin: top;
      transition: transform 0.6s cubic-bezier(0.4, 0, 0.2, 1);
    }
    .envelope-open .envelope-flap {
      transform: rotateX(180deg);
    }
  </style>
