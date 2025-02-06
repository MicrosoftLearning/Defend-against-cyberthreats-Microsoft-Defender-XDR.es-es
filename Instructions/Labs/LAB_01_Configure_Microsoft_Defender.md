---
lab:
  title: "Configuración de Microsoft\_Defender"
  module: Configure the Microsoft Defender XDR environment
---
Imagine que es un analista de operaciones de seguridad que trabaja en una empresa que está implementando Microsoft Defender XDR. Tu rol es guiar al equipo de TI de la empresa para defenderse contra amenazas con Microsoft Defender (XDR). A los ejecutivos de la empresa les preocupa especialmente que se sigan todas las directrices y se cumplan todos los requisitos a la hora de completar las actividades en su entorno.

# Configuración del entorno de Microsoft Defender XDR

En este ejercicio, aprovisionarás el entorno Microsoft Defender XDR, incorporarás estaciones de trabajo de cliente en Defender para punto de conexión y realizarás un escenario de ataque simulado en una estación de trabajo cliente.

Este ejercicio debería tardar en completarse aproximadamente **10 - 15** minutos.

>**Importante:** deberás tener acceso a un inquilino de Microsoft 365 E5 con una licencia de Microsoft Defender para punto de conexión P2 para realizar los ejercicios. También deberás tener estaciones de trabajo cliente de Microsoft Windows 10 o 11 para incorporar y realizar ataques simulados.

## Tarea 1: Preparación del área de trabajo de Microsoft Defender XDR

1. En el explorador Microsoft Edge, ve al portal de Microsoft Defender en (<https://security.microsoft.com>).
1. En el portal de **Microsoft Defender** en el menú de navegación, seleccione **Inicio** a la izquierda.

    >**Nota:** es posible que tengas que desplazarte hasta la parte superior del menú.

1. Desplácese por los elementos del menú hasta **Activos** y seleccione **Dispositivos**.

1. El proceso para implementar el área de trabajo de Defender XDR debería comenzar y debería ver mensajes que digan *cargando e Inicializando* brevemente en la parte superior de la página, y luego va a ver una imagen de una taza de café y un mensaje que dice: **¡Espera! Preparamos nuevos espacios para sus datos y los conectamos.** Tarda aproximadamente 5 minutos en finalizar. *Deje abierta la página y asegúrese de que finaliza, ya que es necesario para el siguiente laboratorio.*

    >**Nota:** ignora los mensajes de error emergentes que indican que *algunos de los datos no se pueden recuperar*. Si el mensaje "Espere, se están preparando nuevos espacios para tus datos y conectándolos" no aparece, o bien se abre la página "Configuración > Microsoft Defender XDR > Cuenta", pero aparece el mensaje *Error al cargar la ubicación del almacenamiento de datos. Inténtalo de nuevo más tarde*, selecciona "Configuración del servicio de alertas" en el menú "General".

1. Cuando la nueva inicialización del área de trabajo se complete correctamente, la página **Inicio** del portal principal mostrará un banner de **Obtención de SIEM y XDR en un solo lugar**. Además, en **Configuración**, la configuración general de Microsoft Defender XDR para la cuenta, las notificaciones por correo electrónico, las **características en versión preliminar**, la configuración del servicio de alertas, los permisos y los roles y la API de streaming están ahora activadas.

### Tarea 2: aplicar directivas de seguridad preestablecidas en Microsoft Defender para Office 365

En esta tarea, asignará directivas de seguridad preestablecidas para Exchange Online Protection (EOP) y Microsoft Defender para Office 365 en el portal de seguridad de Microsoft 365.

1. Inicia sesión en la máquina virtual WIN1 como administrador con la contraseña: **Pa55w.rd**.  

1. Abre el explorador Microsoft Edge.

1. En el explorador Microsoft Edge, ve al portal de Microsoft Defender XDR en (<https://security.microsoft.com>).

1. En el cuadro de diálogo **Iniciar sesión**, copia y pega la cuenta de correo electrónico del inquilino del nombre de usuario de administrador que ha facilitado el proveedor de hospedaje de laboratorio y luego selecciona **Siguiente**.

1. En el cuadro de diálogo **Escribir contraseña**, copia y pega la contraseña de inquilino del administrador que ha facilitado el proveedor de hospedaje del laboratorio y luego selecciona **Iniciar sesión**.

    >**Nota:** si recibes un mensaje "La operación no se ha podido completar. Inténtelo de nuevo más tarde. Si el persiste el problema, ponte en contacto con el Soporte técnico de Microsoft." y haz clic en **Aceptar** para continuar.  

1. Si se muestra, cierre la ventana emergente de visita rápida de Microsoft Defender XDR. **Sugerencia:** Más adelante en este laboratorio, tendrá que esperar hasta que se aprovisione el área de trabajo de Defender, tiempo que puede aprovechar para navegar por las visitas guiadas a fin de obtener más información sobre Microsoft Defender XDR.

1. En el menú de navegación, en el área *Correo electrónico y colaboración*, selecciona **Directivas y reglas**.

1. En el panel *Directiva y reglas*, selecciona **Directivas de amenazas**.

1. En el panel *Directivas de amenazas*, selecciona **Directivas de seguridad preestablecidas**.

    >**Nota:** si recibes el mensaje *"Error de cliente - Error al obtener la regla bip",* selecciona **Aceptar** para continuar. El error se debe al estado de hidratación del inquilino en Office 365, que no está habilitado de forma predeterminada.

    >**Nota:** si recibes el mensaje *"Error de cliente: error al recuperar directivas de seguridad preestablecidas. Vuelve a intentarlo más tarde".* Selecciona **Aceptar** para continuar. Actualiza el explorador mediante **Ctrl+F5**.

1. En la página *emergente* **Información sobre las directivas de seguridad preestablecidas**, selecciona **Cerrar**.

1. En *Protección estándar*, selecciona **Administrar configuración de protección**. **Sugerencia:** si ves esta opción atenuada, actualiza el explorador mediante **Ctrl+F5**.

1. En la sección *Aplicar protección de Exchange Online*, selecciona **Destinatarios específicos** y en **Dominios**, empieza a escribir el nombre de dominio del inquilino, selecciónalo y luego selecciona **Siguiente**.

    >**Sugerencia:** el nombre de dominio del inquilino es el mismo que tiene para la cuenta de administrador, que podría ser algo similar a *WWLx######.onmicrosoft.com*. Ten en cuenta que esta configuración aplica directivas para antispam, filtro de correo no deseado saliente, antimalware, protección contra suplantación de identidad.

1. En la sección *Aplicar protección de Defender para Office 365*, aplica la misma configuración que el paso anterior y selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para protección contra suplantación de identidad, datos adjuntos seguros, vínculos seguros.

1. En la sección *Protección contra suplantación*, selecciona **Siguiente** cuatro veces (4x) para continuar.

1. En la sección *Modo de directiva*, asegúrate de que está seleccionado el botón de selección **Activar la directiva al finalizar** y luego selecciona **Siguiente**.

1. Lee el contenido en *Revise y confirme los cambios* y selecciona **Confirmar** para aplicar los cambios y luego selecciona **Listo** para finalizar.

    >**Nota:** si recibes el mensaje *"El URI <https://outlook.office365.com/psws/service.svc/AntiPhishPolicy>" no es válido para la operación PUT. El URI debe dirigir a un único recurso para las operaciones PUT".* simplemente selecciona **Aceptar** y **Cancelar** para volver a la página principal. Verás que la opción *La protección estándar está activada* está habilitada.

1. En *Protección estricta*, selecciona **Administrar la configuración de protección**. **Sugerencia:** *protección estricta* se encuentra en "Correo electrónico y colaboración - Directivas y reglas - Directivas de amenazas - Directivas de seguridad preestablecidas".

1. En *Aplicar Exchange Online Protection*, selecciona **Destinatarios específicos** y en **Grupos** empieza a escribir **Liderazgo**, selecciónalo y luego selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para antispam, filtro de correo no deseado saliente, antimalware, protección contra suplantación de identidad.

1. En la sección *Aplicar protección de Defender para Office 365*, aplica la misma configuración que el paso anterior y selecciona **Siguiente**. Ten en cuenta que esta configuración aplica directivas para protección contra suplantación de identidad, datos adjuntos seguros, vínculos seguros.

1. En la sección *Protección contra suplantación*, selecciona **Siguiente** cuatro veces (4x) para continuar.

1. En la sección *Modo de directiva*, asegúrate de que está seleccionado el botón de selección **Activar la directiva al finalizar** y luego selecciona **Siguiente**.

1. Lee el contenido en *Revise y confirme los cambios* y selecciona **Confirmar** para aplicar los cambios y luego selecciona **Listo** para finalizar.

    >**Nota:** si recibes el mensaje *"El URI <https://outlook.office365.com/psws/service.svc/AntiPhishPolicy>" no es válido para la operación PUT. El URI debe dirigir a un único recurso para las operaciones PUT".* simplemente selecciona **Aceptar** y **Cancelar** para volver a la página principal. Verás que la opción *Protección estricta está activada* está habilitada.

## Has completado el laboratorio
