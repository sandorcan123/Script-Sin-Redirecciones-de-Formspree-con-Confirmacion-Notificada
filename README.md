# Script Sin Redirecciones de Formspree con Confirmación Notificada

Este repositorio contiene un script JavaScript que facilita el envío de formularios utilizando Formspree como servicio de envío de correos electrónicos. El script está diseñado para mostrar una notificación al usuario después del envío del formulario y evitar redirecciones automáticas a la página de confirmación de Formspree, lo que proporciona una experiencia de usuario mejorada.

## Funcionalidades

- Envío de formulario utilizando Formspree.
- Muestra una notificación al usuario sobre el resultado del envío.
- Evita redirecciones automáticas a la página de confirmación de Formspree.

## Uso

Simplemente integra el siguiente script en tu página web donde se encuentre el formulario que deseas enviar utilizando Formspree. Asegúrate de actualizar la URL de la acción del formulario con la URL de tu formulario de Formspree.

```javascript
document.addEventListener("DOMContentLoaded", function() {
    var form = document.getElementById("contactForm");

    form.addEventListener("submit", function(event) {
        event.preventDefault();

        fetch(form.action, {
            method: form.method,
            body: new FormData(form),
            headers: {
                'Accept': 'application/json'
            }
        })
        .then(response => {
            if (response.ok) {
                alert("¡El correo fue enviado exitosamente!");
                form.reset(); // Limpiar el formulario después de enviarlo
            } else {
                throw new Error('Error en el envío del formulario');
            }
        })
        .catch(error => {
            console.error('Error:', error);
            alert("Hubo un error al enviar el correo. Por favor, inténtalo nuevamente.");
        });
    });
});

