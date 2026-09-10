# EasySpace

Landing page di [EasySpace](https://micheleruccidev.github.io/Easy-Space/) — sviluppo web, app e identità digitale.

## Sviluppo locale

```bash
python3 -m http.server 43123
```

Apri [http://127.0.0.1:43123](http://127.0.0.1:43123).

## Perché da telefono era tutto bianco

Su iPhone / browser in-app (WhatsApp, Instagram) la pagina restava bianca per tre cause insieme:

1. **Script bloccanti in `<head>`** (`cdn.tailwindcss.com` e `unpkg.com/lucide`) prima di qualsiasi CSS. Finché i CDN non rispondevano, il browser mostrava lo sfondo bianco di default.
2. **Blur GPU pesantissimi** (`filter: blur(140px)` su orbs fissi, `backdrop-filter` sulla navbar sticky, `feGaussianBlur` nell’SVG). Su Safari iOS il compositor va in crash e ridipinge tutta la pagina di bianco.
3. **Intro a schermo intero** che aspettava `window.load` e, se Lucide andava in errore, bloccava anche lo scroll.

Il fix: CSS scuro immediato, icone in fondo pagina, glow senza blur live su mobile, intro con timeout di sicurezza.
