# Ruleta Quiz Online (Host + Jugadores)
Multiusuario en tiempo real con Firebase (solo frontend).

## Archivos
- `host.html`: Vista del docente para crear sala, controlar preguntas y ver ranking top 5.
- `join.html`: Vista para estudiantes (móvil/PC). Se unen con PIN y responden.
- `questions.json`: Ejemplo de banco de preguntas.
- (Este proyecto funciona solo con un proyecto de Firebase y Realtime Database habilitado).

## Pasos rápidos
1. Crea un proyecto en https://console.firebase.google.com
2. Agrega una app web y copia la **configuración** (apiKey, authDomain, etc.).
3. Habilita **Realtime Database** (modo test o con reglas simples de lectura/escritura para `rooms/*`).
4. Abre `host.html` y `join.html` y pega tu configuración en el bloque marcado `// 1) PASTE YOUR CONFIG HERE`.
5. Sube estos archivos a un hosting estático (GitHub Pages, Netlify, Vercel) o ábrelos localmente.
6. En `host.html`, pega o carga tu banco de preguntas en formato JSON:
   ```json
   [
     {"texto":"¿...?", "opciones":["A","B","C","D"], "correcta":2}
   ]
   ```
7. Presiona **Crear sala** → se genera un PIN y URL para unirse.
8. Estudiantes abren `join.html?pin=XXXXXX`, escriben su nombre y se unen.
9. En el host: **Iniciar pregunta** → cuentan los segundos → **Mostrar correcta** → asigna puntos automáticos.
10. **Siguiente** avanza a la siguiente pregunta. **Finalizar** muestra ranking final.

## Puntuación
- +100 por respuesta correcta (puedes ajustar en `host.html`, función `revealCorrect`).

## Seguridad de reglas (opcional)
En Realtime Database Rules podrías limitar escritura de `players` y `answers` por PIN:
```json
{
  "rules": {
    "rooms": {
      "$pin": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```
Ajusta según tus necesidades.
