# Subir cambios a GitHub sin errores

## Errores frecuentes y qué hacer

### 1. "Authentication failed" o "Support for password authentication was removed"
**Causa:** GitHub ya no acepta contraseña por HTTPS.  
**Solución:** Usar un **Personal Access Token (PAT)** en lugar de la contraseña.

- Ve a GitHub → Settings → Developer settings → Personal access tokens.
- Genera un token (classic) con al menos `repo`.
- Cuando Git pida contraseña, pega el **token**, no tu contraseña de GitHub.

### 2. "Permission denied" o "403"
**Causa:** No tienes permiso de escritura en el repo (o el token no tiene permisos).  
**Solución:** Confirma que eres colaborador del repo `clickcommercemx/tandamas-landing` y que el token tiene permiso `repo`.

### 3. Muchos archivos "modified" sin haberlos tocado
**Causa:** Diferencias de saltos de línea (CRLF en Windows vs LF en GitHub).  
**Solución:** El archivo `.gitattributes` de este repo ya normaliza esto. Después de hacer `git add` y `git commit`, esos cambios fantasma deberían desaparecer en los próximos commits.

### 4. "Failed to push" / "Updates were rejected"
**Causa:** En GitHub hay commits que tú no tienes (alguien más subió cambios).  
**Solución:** Antes de hacer push, traer y unir los cambios:

```bash
git pull origin main --rebase
git push origin main
```

### 5. Conflictos al hacer pull
**Causa:** Tú y otro (o tú en otra PC) modificaron las mismas líneas.  
**Solución:** Abre los archivos que marque Git como "both modified", resuelve las marcas `<<<<<<<`, `=======`, `>>>>>>>`, guarda, luego:

```bash
git add .
git rebase --continue
```
o si usaste `git pull` sin `--rebase`:
```bash
git add .
git commit -m "Resuelvo conflictos"
git push origin main
```

---

## Flujo recomendado cada vez que quieras subir cambios

Abre terminal (PowerShell o CMD) en la carpeta del proyecto y ejecuta:

```bash
cd c:\Users\Dan1\Documents\landing1n\tandamas-landing

git status
git add .
git status
git commit -m "Descripción breve del cambio"
git pull origin main --rebase
git push origin main
```

- Si `git push` pide usuario y contraseña: usa tu usuario de GitHub y el **Personal Access Token** (no la contraseña de la cuenta).

---

## Si sigues con errores

Copia el **mensaje de error completo** (o una captura) y compártelo para ver el caso concreto.
