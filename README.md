# Custom Apps

Colección de aplicaciones personalizadas. Este es el repo padre que contiene referencias a todos los proyectos.

## 📦 Repos incluidos

- **[agent-editor](https://github.com/Pablouski7/agent-editor)** - Editor de agentes
- **[ticktick-map-app](https://github.com/Pablouski7/ticktick-map-app)** - App de mapeo de TickTick
- **[video-editor](https://github.com/Pablouski7/video-editor)** - Editor de video

## 🚀 Primeros pasos

### Clonar el repo padre
```bash
git clone https://github.com/Pablouski7/custom-apps.git
cd custom-apps
```

### Clonar todos los repos
```bash
# Opción 1: Clonar todos en subdirectorios
git clone https://github.com/Pablouski7/agent-editor.git
git clone https://github.com/Pablouski7/ticktick-map-app.git
git clone https://github.com/Pablouski7/video-editor.git

# Opción 2: Usar el script de clonación (ver abajo)
bash clone-all.sh
```

## 📝 Scripts útiles

### `clone-all.sh` - Clonar todos los repos
```bash
#!/bin/bash
REPOS=(
  "agent-editor"
  "ticktick-map-app"
  "video-editor"
)

for repo in "${REPOS[@]}"; do
  echo "Clonando $repo..."
  git clone https://github.com/Pablouski7/$repo.git
done
echo "✅ Todos los repos clonados"
```

Ejecutar:
```bash
bash clone-all.sh
```

### Actualizar todos los repos
```bash
# Opción 1: Actualizar cada repo por separado
cd agent-editor && git pull origin main && cd ..
cd ticktick-map-app && git pull origin main && cd ..
cd video-editor && git pull origin main && cd ..

# Opción 2: Usar este script
for dir in agent-editor ticktick-map-app video-editor; do
  if [ -d "$dir" ]; then
    echo "Actualizando $dir..."
    cd "$dir"
    git pull origin main
    cd ..
    echo "✅ $dir actualizado"
  fi
done
```

### Verificar estado de todos los repos
```bash
for dir in agent-editor ticktick-map-app video-editor; do
  if [ -d "$dir" ]; then
    echo ""
    echo "=== $dir ==="
    cd "$dir"
    git status
    cd ..
  fi
done
```

### Hacer commit y push en todos los repos
```bash
for dir in agent-editor ticktick-map-app video-editor; do
  if [ -d "$dir" ]; then
    echo "Pusheando cambios en $dir..."
    cd "$dir"
    git add .
    git commit -m "$1"  # Mensaje como argumento
    git push origin main
    cd ..
    echo "✅ $dir pusheado"
  fi
done

# Usar: bash push-all.sh "tu mensaje de commit"
```

## 📋 Flujo típico de trabajo

### 1. Actualizar todos los repos
```bash
for dir in agent-editor ticktick-map-app video-editor; do
  [ -d "$dir" ] && cd "$dir" && git pull origin main && cd ..
done
```

### 2. Hacer cambios en un repo
```bash
cd nombre-del-repo
# ... hacer cambios ...
git add .
git commit -m "descripción de cambios"
git push origin main
```

### 3. Ver estado global
```bash
for dir in agent-editor ticktick-map-app video-editor; do
  [ -d "$dir" ] && echo "=== $dir ===" && cd "$dir" && git log --oneline -n 3 && cd ..
done
```

## 🔄 Alias útiles (opcional)

Agrega a tu `~/.bashrc` o `~/.zshrc`:

```bash
# Actualizar todos los repos
alias update-all='for dir in agent-editor ticktick-map-app video-editor; do [ -d "$dir" ] && (cd "$dir" && git pull origin main && echo "✅ $dir") || true; done'

# Ver estado de todos
alias status-all='for dir in agent-editor ticktick-map-app video-editor; do [ -d "$dir" ] && echo "=== $dir ===" && (cd "$dir" && git status); done'

# Ver logs de todos
alias log-all='for dir in agent-editor ticktick-map-app video-editor; do [ -d "$dir" ] && (cd "$dir" && echo "=== $dir ===" && git log --oneline -n 3); done'
```

Luego puedes usar:
```bash
update-all
status-all
log-all
```

## 📂 Estructura
```
custom-apps/
├── README.md (este archivo)
├── agent-editor/ (repo clonado)
├── ticktick-map-app/ (repo clonado)
└── video-editor/ (repo clonado)
```
