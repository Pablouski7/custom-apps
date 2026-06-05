# Custom Apps

Colección de aplicaciones personalizadas. Este es el repo padre que contiene referencias a todos los proyectos.

## 📦 Repos incluidos

- **[agent-editor](https://github.com/Pablouski7/agent-editor)** - Editor de agentes
- **[ticktick-map-app](https://github.com/Pablouski7/ticktick-map-app)** - App de mapeo de TickTick
- **[video-editor](https://github.com/Pablouski7/video-editor)** - Editor de video

## 🚀 Primeros pasos

### Clonar el repo padre con todos los subrepos
Los subrepos están incluidos como **git submodules**, así que todo viene junto:

```bash
# Primera vez: clonar con submodules
git clone --recurse-submodules https://github.com/Pablouski7/custom-apps.git
cd custom-apps
```

Si ya tienes el repo clonado sin submodules:
```bash
git submodule update --init --recursive
```

## 📝 Comandos útiles

### Actualizar todos los repos (incluido el padre)
```bash
# Actualizar el repo padre y todos los submodules
git pull origin main
git submodule update --remote --merge
```

O de forma más completa:
```bash
# Actualizar repo padre
git pull origin main

# Actualizar todos los submodules
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

### 1. Clonar todo (primera vez)
```bash
git clone --recurse-submodules https://github.com/Pablouski7/custom-apps.git
cd custom-apps
```

### 2. Actualizar todo
```bash
git pull origin main
git submodule update --remote --merge
```

### 3. Hacer cambios en un subrepo
```bash
cd nombre-del-subrepo  # agent-editor, ticktick-map-app o video-editor
# ... hacer cambios ...
git add .
git commit -m "descripción de cambios"
git push origin main
cd ..

# Actualizar el repo padre para que refleje el nuevo commit del submodule
git add nombre-del-subrepo
git commit -m "chore: actualizar referencia de nombre-del-subrepo"
git push origin main
```

### 4. Ver estado global
```bash
# Estado del repo padre y submodules
git status

# Logs de todos
for dir in agent-editor ticktick-map-app video-editor; do
  [ -d "$dir" ] && (cd "$dir" && echo "=== $dir ===" && git log --oneline -n 3)
done
```

## 🔄 Alias útiles (opcional)

Agrega a tu `~/.bashrc` o `~/.zshrc`:

```bash
# Actualizar todo (padre + submodules)
alias update-all='git pull origin main && git submodule update --remote --merge && echo "✅ Todo actualizado"'

# Ver estado de todos
alias status-all='git status && echo "" && for dir in agent-editor ticktick-map-app video-editor; do [ -d "$dir" ] && echo "=== $dir ===" && (cd "$dir" && git status); done'

# Ver logs de todos
alias log-all='git log --oneline -n 3 && echo "" && for dir in agent-editor ticktick-map-app video-editor; do [ -d "$dir" ] && (cd "$dir" && echo "=== $dir ===" && git log --oneline -n 3); done'
```

Luego puedes usar:
```bash
update-all      # Actualizar todo en un comando
status-all      # Ver estado de todos
log-all         # Ver logs de todos
```

## 📂 Estructura
```
custom-apps/
├── .gitmodules (configuración de submodules)
├── README.md (este archivo)
├── agent-editor/ (submodule → repo independiente)
├── ticktick-map-app/ (submodule → repo independiente)
└── video-editor/ (submodule → repo independiente)
```

### ¿Cómo funcionan los submodules?

Los submodules te permiten:
- ✅ Clonar todo junto: `git clone --recurse-submodules https://...`
- ✅ Trabajar en cada repo de forma independiente
- ✅ El repo padre referencia un commit específico de cada subrepo
- ✅ Actualizar cada subrepo sin afectar el padre (a menos que lo confirmes)

Para más info: https://git-scm.com/book/es/v2/Herramientas-de-Git-Submódulos
