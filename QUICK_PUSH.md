# 🚀 PUSH A GITHUB - INSTRUCCIONES RÁPIDAS

## ⚡ 3 PASOS SIMPLES

### PASO 1: Crear Repositorio en GitHub (en navegador)

1. Ir a: https://github.com/new
2. Nombre: `Sesion - 5 - 2025 - CodeIA`
3. Descripción: `Restaurant Management System - NestJS Backend`
4. Presionar: **Create repository**
5. ⚠️ **NO inicializar** con README, gitignore, o licencia

### PASO 2: Ejecutar en PowerShell

Reemplaza `TU_USUARIO` con tu usuario de GitHub:

```powershell
$env:Path += ";C:\Program Files\Git\bin"
cd "c:\Websites v2\CodeIA\backend-nest"
git remote add origin https://github.com/TU_USUARIO/Sesion-5-2025-CodeIA.git
git push -u origin main
git push origin v0.1.0
```

### PASO 3: Verificar en GitHub

Entra a: https://github.com/TU_USUARIO/Sesion-5-2025-CodeIA

Deberías ver:
- ✅ Rama `main` con 5 commits
- ✅ README.md visible
- ✅ Carpeta `docs/e4/` con documentación
- ✅ Tag `v0.1.0`

---

## 🔐 Autenticación

Cuando Git te pida contraseña, usa un **Personal Access Token**:

1. Ir a: https://github.com/settings/tokens/new
2. Seleccionar: `repo` y `workflow`
3. Crear token
4. Copiar y usar como contraseña (en lugar de tu contraseña de GitHub)

---

## 📊 Estado Actual

| Métrica | Valor |
|---------|-------|
| Rama | main |
| Commits | 5 |
| Archivos | 16 |
| Tag | v0.1.0 |
| Documentación | 170+ págs |
| Modelos BD | 12 |
| Endpoints API | 22 |
| Status | ✅ Listo |

---

**Listo para ejecutar. ¡A por el push!** 🎉
