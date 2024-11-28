---
title: Git - Trucos avanzados para mejorar tu flujo de trabajo
date: 2024/11/28
description: Mejora tu flujo de trabajo con estos trucos avanzados de Git para un manejo eficiente del control de versiones.
tag: Git
author: Farley Piedrahita Orozco
---

Git es una herramienta esencial para cualquier desarrollador, y aunque los comandos básicos como `git add`, `git commit`, y `git push` son indispensables, hay funciones avanzadas que pueden optimizar significativamente tu flujo de trabajo. En este post, exploraremos algunos trucos útiles para que aproveches al máximo Git.  

---

#### **1. Usa alias para comandos frecuentes**  
Escribir comandos largos puede ser tedioso, pero con alias, puedes simplificar las cosas. Configúralos en tu archivo global de configuración:  
```bash  
git config --global alias.st status  
git config --global alias.co checkout  
git config --global alias.br branch  
git config --global alias.cm commit  
```  
Ahora, en lugar de escribir `git status`, solo necesitas `git st`.  

---

#### **2. Recupera cambios eliminados con `git reflog`**  
¿Has borrado un branch o commit accidentalmente? No te preocupes, con `git reflog` puedes recuperarlo.  

1. Ve al historial de referencias:  
   ```bash  
   git reflog  
   ```  
2. Encuentra el hash del commit perdido y recupéralo:  
   ```bash  
   git checkout <hash>  
   ```  

---

#### **3. Trabaja con `git stash` para guardar cambios temporales**  
A veces necesitas cambiar de branch rápidamente pero no quieres perder tus cambios actuales. Usa `git stash` para guardarlos temporalmente.  

1. Guarda los cambios en un stash:  
   ```bash  
   git stash  
   ```  
2. Vuelve a aplicarlos más tarde:  
   ```bash  
   git stash apply  
   ```  
3. Revisa la lista de stashes:  
   ```bash  
   git stash list  
   ```  

---

#### **4. Usa `git cherry-pick` para integrar cambios específicos**  
Cuando solo necesitas un commit específico de otro branch, `git cherry-pick` es tu aliado.  

1. Encuentra el hash del commit que necesitas:  
   ```bash  
   git log branch-destino  
   ```  
2. Aplica el commit al branch actual:  
   ```bash  
   git cherry-pick <hash>  
   ```  

---

#### **5. Limpia tu historial con `git rebase -i`**  
Si tu historial de commits se ve desordenado, puedes limpiarlo con un rebase interactivo.  

1. Inicia un rebase interactivo:  
   ```bash  
   git rebase -i HEAD~n  
   ```  
   *(Reemplaza `n` con el número de commits que quieres editar).*  
2. Cambia "pick" por "squash" para combinar commits o "edit" para modificar mensajes.  

---

#### **6. Soluciona conflictos de merge fácilmente**  
Los conflictos son inevitables, pero puedes resolverlos eficientemente:  

1. Cuando ocurre un conflicto, Git marcará los archivos problemáticos. Abre el archivo y busca marcas como:  
   ```  
   <<<<<<< HEAD  
   Cambios en tu branch  
   =======  
   Cambios en el branch fusionado  
   >>>>>>> branch-nombre  
   ```  
2. Edita el archivo y elimina las marcas, manteniendo el código correcto.  

Luego, añade los cambios y finaliza el merge:  
```bash  
git add archivo  
git commit  
```  

---

#### **7. Usa `git log` como un pro**  
El comando `git log` puede personalizarse para obtener información más clara y útil. Por ejemplo:  

- Para un historial simplificado:  
  ```bash  
  git log --oneline --graph --decorate --all  
  ```  
- Filtrar por autor:  
  ```bash  
  git log --author="Farley"  
  ```  

---

#### **8. Trabaja con submódulos**  
Si tu proyecto incluye otro repositorio como dependencia, puedes usar submódulos para gestionarlo.  

1. Añade un submódulo:  
   ```bash  
   git submodule add <url-del-repo>  
   ```  
2. Actualiza los submódulos:  
   ```bash  
   git submodule update --init --recursive  
   ```  

---

#### **9. Automatiza tareas con hooks de Git**  
Los hooks son scripts que se ejecutan automáticamente en eventos específicos de Git, como un commit o un push.  

Por ejemplo, crea un hook en `.git/hooks/pre-commit` para verificar errores de estilo antes de cada commit:  
```bash  
#!/bin/bash  
phpcs --standard=PSR12 ./src  
if [ $? -ne 0 ]; then  
    echo "Errores de estilo detectados. Corrígelos antes de commitear."  
    exit 1  
fi  
```  
Haz que el archivo sea ejecutable:  
```bash  
chmod +x .git/hooks/pre-commit  
```  

---

#### **10. Limpia el repositorio con `git clean`**  
¿Tu proyecto está lleno de archivos no rastreados? Usa `git clean` para eliminarlos rápidamente:  

1. Ve qué se eliminaría (modo seguro):  
   ```bash  
   git clean -n  
   ```  
2. Elimina los archivos no rastreados:  
   ```bash  
   git clean -f  
   ```  

---

### **Conclusión**  
Estos trucos avanzados pueden ahorrarte tiempo y mejorar tu flujo de trabajo. Explora cada uno y descubre cómo integrarlos en tu día a día como desarrollador.  

¿Qué truco te pareció más útil? Si tienes algún otro consejo avanzado de Git, compártelo conmigo escribiendo a **farchodev@gmail.com**. 😊