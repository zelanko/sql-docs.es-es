---
title: Configuración de Correo electrónico de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- Sql12.swb.sqlimail.newaccount.f1
- Sql12.swb.sqlimail.manageexistingaccount.f1
- Sql12.swb.dbmail.manageexistingaccount.f1
- Sql12.swb.sqlimail.manageexistingprofile.f1
- Sql12.swb.sqlimail.newprofile.f1
- Sql12.swb.sqlimail.profileandaccountmanagement.f1
- Sql12.swb.dbmail.configuresystem.f1
- Sql12.swb.dbmail.profileandaccountmanagement.f1
- Sql12.swb.dbmail. manageprofilesecurity.profileview.f1
- Sql12.swb.dbmail.selectconfiguration.f1
- Sql12.swb.dbmail.newsqlimailaccount.f1
- Sql12.swb.sqlimail.manageprofilesecurity.profileview.f1
- Sql12.swb.sqlimail.newsqlimailaccount.f1
- Sql12.swb.dbmail.newaccount.f1
- Sql12.swb.dbmail.manageexistingprofile.f1
- Sql12.swb.sqlimail.configuresystem.f1
- Sql12.swb.sqlimail.selectconfiguration.f1
- Sql12.swb.dbmail.completewizard.f1
- Sql12.swb.sqlimail.welcome.f1
- sql12.swb.dbmail.sendtestemail.f1
- Sql12.swb.sqlimail.addaccounttoprofile.f1
- Sql12.swb.dbmail.welcome.f1
- Sql12.swb.dbmail.newprofile.f1
- Sql12.swb.dbmail.addaccounttoprofile.f1
- sql12.swb.dbmail.sendtestemail.test.f1
- Sql12.swb.sqlimail.completewizard.f1
- Sql12.swb.sqlimail.manageprofilesecurity.principalview.f1
- Sql12.swb.dbmail.manageprofilesecurity.principalview.f1
ms.assetid: 7edc21d4-ccf3-42a9-84c0-3f70333efce6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e480363941d8928d270f978471b5474a8e24b0a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68418875"
---
# <a name="configure-database-mail"></a>Configuración de Correo electrónico de base de datos
  En este tema se describe cómo habilitar y configurar el Correo electrónico de base de datos con el Asistente para configuración de Correo electrónico de base de datos y crear un script de configuración de Correo electrónico de base de datos mediante plantillas.  
  

  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
 Use la opción **DatabaseMail XPs** para habilitar Correo electrónico de base de datos en este servidor. Para obtener más información, vea el tema de referencia [Database Mail XPs (opción de configuración del servidor)](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) .  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 Se necesita un bloqueo de base de datos para habilitar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker en cualquier base de datos. Si se desactivó Service Broker en **msdb**, para habilitar Correo electrónico de base de datos, detenga primero el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que Service Broker pueda obtener el bloqueo necesario.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
 Para configurar Correo electrónico de base de datos, debe ser miembro del rol de servidor fijo **sysadmin** . Para enviar Correo electrónico de base de datos debe ser miembro del rol de base de datos **DatabaseMailUserRole** en la base de datos **msdb** .  
  
##  <a name="using-database-mail-configuration-wizard"></a><a name="SSMSProcedure"></a> Usar el asistente para configuración del Correo electrónico de base de datos  
 **Para configurar Correo electrónico de base de datos con un asistente**  
  
1.  En Explorador de objetos, expanda el nodo de la instancia para la que desea configurar Correo electrónico de base de datos.  
  
2.  Expanda el nodo **Administración** .  
  
3.  Haga clic con el botón derecho en **Correo electrónico de base de datos**y haga clic en **Configurar Correo electrónico de base de datos**.  
  
4.  Complete los cuadros de diálogo del asistente.  
  

  
  
  
###  <a name="welcome-page"></a><a name="Welcome"></a>Página principal  
 En esta página se describen los pasos para configurar Correo electrónico de base de datos.  
  
 **No volver a mostrar esta página** : Active esta casilla para omitir la visualización de esta página de bienvenida en el futuro.  
  
 **Siguiente** : continúa con la página **Seleccionar una tarea de configuración** .  
  
 **Cancelar** : termina el asistente sin configurar correo electrónico de base de datos  
  
 
  
###  <a name="select-configuration-task"></a><a name="ConfigTask"></a>Seleccionar tarea de configuración  
 Use la página **Seleccionar tarea de configuración** para indicar qué tarea se completará cada vez que se use el Asistente. Si cambia de opinión antes de completar el Asistente, utilice el botón **Atrás** para volver a esta página y seleccionar otra tarea.  
  
> [!NOTE]  
>  Si no se ha habilitado el Correo electrónico de base de datos, recibirá el mensaje **La característica Correo electrónico de base de datos no está disponible.  ¿Quiere habilitar esta característica?** Responder **Sí**es equivalente a habilitar Correo electrónico de base de datos con la [opción Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) del procedimiento almacenado del sistema **sp_configure** .  
  
 **Instalar Correo electrónico de base de datos realizando las siguientes tareas**  
 Realiza todas las tareas necesarias para configurar el Correo electrónico de base de datos por primera vez. Esta opción incluye las otras tres.  
  
 **Administrar cuentas y perfiles de Correo electrónico de base de datos**  
 Permite crear nuevas cuentas y perfiles de Correo electrónico de base de datos, así como visualizar, cambiar o eliminar los ya existentes.  
  
 **Administrar seguridad del perfil**  
 Permite configurar qué usuarios tienen acceso a los perfiles de Correo electrónico de base de datos.  
  
 **Ver o cambiar parámetros del sistema**  
 Permite configurar los parámetros del sistema de Correo electrónico de base de datos, como el tamaño máximo de los datos adjuntos.  
  

  
###  <a name="new-account-page"></a><a name="NewAccount"></a>Página nueva cuenta  
 Use esta página para crear una nueva cuenta de Correo electrónico de base de datos. Esta cuenta contiene información para enviar correo electrónico a un servidor SMTP.  
  
 Las cuentas de Correo electrónico de base de datos contienen la información que utiliza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para enviar mensajes de correo electrónico a un servidor SMTP. Cada cuenta contiene información para un servidor de correo electrónico.  
  
 Una cuenta del Correo electrónico de base de datos solo se utiliza para el Correo electrónico de base de datos. Estas cuentas no corresponden a cuentas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ni de Microsoft Windows. Correo electrónico de base de datos se puede enviar mediante las credenciales del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], mediante otras credenciales que suministre o en forma anónima. Cuando se utiliza la autenticación básica, el nombre de usuario y la contraseña de una cuenta del Correo electrónico de base de datos solo se utilizan para la autenticación con el servidor de correo electrónico. No es necesario que una cuenta corresponda a un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a un usuario del equipo en el que se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Nombre de cuenta**  
 Escriba el nombre de la nueva cuenta.  
  
 **Descripción**  
 Escriba una descripción de la cuenta. La descripción es opcional.  
  
 **Dirección de correo electrónico**  
 Escriba el nombre de la dirección de correo electrónico de la cuenta. Es la dirección desde la que se envía el correo electrónico. Por ejemplo, una cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede enviar correo electrónico desde la dirección SqlAgent@Adventure-Works.com.  
  
 **Nombre para mostrar**  
 Escriba el nombre que se muestra en los mensajes de correo electrónico enviados desde esta cuenta. Este nombre es opcional. Se trata del nombre que se muestra en los mensajes enviados desde esta cuenta. Por ejemplo, una cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede mostrar el nombre "SQL Server Agent Automated Mailer" (Proveedor de servicio de envío de correo automatizado del Agente SQL Server) en los mensajes de correo electrónico.  
  
 **Correo electrónico de respuesta**  
 Escriba la dirección de correo electrónico que se utilizará para las respuestas a los mensajes enviados desde esta cuenta. Esta dirección es opcional. Por ejemplo, las respuestas a los mensajes de una cuenta del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden dirigirse al administrador de la base de datos, danw@Adventure-Works.com.  
  
 **Nombre del servidor**  
 Escriba el nombre o la dirección IP del servidor SMTP que utiliza la cuenta para enviar correo electrónico. Normalmente, está en un formato similar a `smtp.` *<your_company>* `.com`. Si necesita ayuda, consulte a su administrador de correo.  
  
 **Número de puerto**  
 Escriba el número de puerto del servidor SMTP de esta cuenta. La mayor parte de los servidores SMTP utilizan el puerto 25.  
  
 **Este servidor requiere una conexión segura (SSL)**  
 Cifra comunicación mediante SSL (Capa de sockets seguros).  
  
 **Autenticación de Windows con credenciales del servicio Motor de base de datos**  
 Se establece la conexión al servidor SMTP mediante credenciales configuradas para el servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticación básica**  
 Se especifica el nombre de usuario y la contraseña que requiere el servidor SMTP.  
  
 **Nombre de usuario**  
 Escriba el nombre de usuario que utiliza el Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, el nombre de usuario es necesario.  
  
 **Contraseña**  
 Escriba la contraseña que utiliza el Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, la contraseña es necesaria.  
  
 **Confirmar contraseña**  
 Escriba de nuevo la contraseña para confirmarla. Si el servidor SMTP requiere autenticación básica, la contraseña es necesaria.  
  
 **Autenticación anónima**  
 Se envía correo al servidor SMTP sin credenciales de inicio de sesión. Utilice esta opción cuando el servidor SMTP no requiere autenticación.  
  
 
  
###  <a name="manage-existing-account-page"></a><a name="ExistingAccount"></a>Página Administrar cuenta existente  
 Utilice esta página para administrar una cuenta existente de Correo electrónico de base de datos.  
  
 **Nombre de cuenta**  
 Seleccione la cuenta que va a ver, actualizar o eliminar.  
  
 **Eliminar**  
 Elimina la cuenta seleccionada. Debe quitar esta cuenta de los perfiles asociados, o eliminar dichos perfiles, antes de eliminar la cuenta seleccionada.  
  
 **Descripción**  
 Muestra o actualiza la descripción de la cuenta. La descripción es opcional.  
  
 **Dirección de correo electrónico**  
 Muestra o actualiza el nombre de la dirección de correo electrónico de la cuenta. Es la dirección desde la que se envía el correo electrónico. Por ejemplo, una cuenta para Microsoft SQL Server agente puede enviar correo electrónico desde la **SqlAgent@Adventure-Works.com**dirección.  
  
 **Nombre para mostrar**  
 Muestra o actualiza el nombre que se muestra en los mensajes de correo electrónico enviados desde esta cuenta. Este nombre es opcional. Se trata del nombre que se muestra en los mensajes enviados desde esta cuenta. Por ejemplo, una cuenta del Agente SQL Server puede mostrar el nombre **SQL Server Agent Automated Mailer (Proveedor de servicio de envío de correo automatizado del Agente SQL Server)** en los mensajes de correo electrónico.  
  
 **Correo electrónico de respuesta**  
 Muestra o actualiza la dirección de correo electrónico que se utilizará para las respuestas a los mensajes enviados desde esta cuenta. Esta dirección es opcional. Por ejemplo, las respuestas a una cuenta de Agente SQL Server pueden dirigirse al administrador de **danw@Adventure-Works.com**la base de datos,.  
  
 **Nombre del servidor**  
 Muestra o actualiza el nombre del servidor SMTP que utiliza la cuenta para enviar correo electrónico. Típicamente está en un formato similar a **smtp.<su_compañía>.com**. Si necesita ayuda, consulte a su administrador de correo.  
  
 **Número de puerto**  
 Muestra o actualiza el número de puerto del servidor SMTP de esta cuenta. La mayor parte de los servidores SMTP utilizan el puerto 25.  
  
 **Este servidor requiere una conexión segura (SSL)**  
 Cifra comunicación mediante SSL (Capa de sockets seguros).  
  
 **Autenticación de Windows con credenciales del servicio Motor de base de datos**  
 Se establece la conexión al servidor SMTP mediante credenciales configuradas para el servicio [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] .  
  
 **Autenticación básica**  
 Se especifica el nombre de usuario y la contraseña que requiere el servidor SMTP.  
  
 **Nombre de usuario**  
 Muestra o actualiza el nombre de usuario que utiliza el Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, el nombre de usuario es necesario.  
  
 **Contraseña**  
 Cambie la contraseña que utiliza el Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, la contraseña es necesaria.  
  
 **Confirmar contraseña**  
 Escriba de nuevo la contraseña para confirmarla. Si el servidor SMTP requiere autenticación básica, la contraseña es necesaria.  
  
 **Autenticación anónima**  
 Se envía correo al servidor SMTP sin credenciales de inicio de sesión. Utilice esta opción cuando el servidor SMTP no requiere autenticación.  
  

  
###  <a name="new-profile-page"></a><a name="NewProfile"></a>Página nuevo perfil  
 Utilice esta página para crear un perfil de Correo electrónico de base de datos. Un perfil del Correo electrónico de base de datos es un conjunto de cuentas del Correo electrónico de base de datos. Los perfiles aumentan la confiabilidad en casos en los que no se puede tener acceso a un servidor de correo electrónico al proporcionar cuentas de Correo electrónico de base de datos alternativas. Se requiere al menos una cuenta de Correo electrónico de base de datos. Para obtener más información acerca de cómo establecer la prioridad de las cuentas de Correo electrónico de base de datos en el perfil, vea [Create a Database Mail Profile](create-a-database-mail-profile.md).  
  
 Utilice los botones **Subir** y **Bajar** para cambiar el orden en que se utilizan las cuentas del Correo electrónico de base de datos. Este orden se determina mediante un valor denominado número de secuencia. El botón**Subir** reduce el número de secuencia y el botón **Bajar** aumenta el número de secuencia. El número de secuencia determina el orden en que el Correo electrónico de base de datos utiliza las cuentas en el perfil. En el caso de un mensaje de correo electrónico nuevo, el Correo electrónico de base de datos se inicia con la cuenta con el número de secuencia más bajo. Si la cuenta genera un error, el Correo electrónico de base de datos utiliza la cuenta con el siguiente número de secuencia superior y así sucesivamente hasta que el Correo electrónico de base de datos envía el mensaje correctamente o la cuenta con el número de secuencia superior genera un error. Si la cuenta con el número de secuencia superior genera un error, el Correo electrónico de base de datos pausa los intentos de envío del correo electrónico durante la cantidad de tiempo configurada en el parámetro **AccountRetryDelay** y, a continuación, inicia nuevamente el proceso de intento de envío del correo electrónico comenzando por el número de secuencia más bajo. Use el parámetro **AccountRetryAttempts** del Correo electrónico de base de datos para configurar el número de veces que el proceso de correo electrónico externo intenta enviar el mensaje de correo electrónico al usar cada cuenta del perfil especificado. Puede configurar los parámetros **AccountRetryDelay** y **AccountRetryAttempts** en la página **Configurar parámetros del sistema** del Asistente para configuración del Correo electrónico de base de datos.  
  
 **Nombre de perfil**  
 Escriba el nombre del nuevo perfil. El perfil se crea con este nombre. No utilice el nombre de un perfil existente.  
  
 **Descripción**  
 Escriba una descripción para el perfil. La descripción es opcional.  
  
 **Cuentas SMTP**  
 Elija una o más cuentas para el perfil. La prioridad establece el orden en el que el Correo electrónico de base de datos utiliza las cuentas. Si no se incluye ninguna cuenta, debe hacer clic en **Agregar** para continuar y agregar una nueva cuenta SMTP.  
  
 **Add (Agregar)**  
 Agregue una cuenta al perfil.  
  
 **Remove**  
 Quite la cuenta seleccionada del perfil.  
  
 **Subir**  
 Aumente la prioridad de la cuenta seleccionada.  
  
 **Bajar**  
 Disminuya la prioridad de la cuenta seleccionada.  
  

  
###  <a name="manage-existing-profile-page"></a><a name="ExistingProfile"></a>Página administrar perfil existente  
 Utilice esta página para administrar un perfil existente del Correo electrónico de base de datos. Un perfil del Correo electrónico de base de datos es un conjunto de cuentas del Correo electrónico de base de datos. Los perfiles aumentan la confiabilidad en casos en los que no se puede tener acceso a un servidor de correo electrónico al proporcionar cuentas de Correo electrónico de base de datos alternativas. Se requiere al menos una cuenta de Correo electrónico de base de datos. Para obtener más información acerca de cómo establecer la prioridad de las cuentas de Correo electrónico de base de datos en el perfil, vea [Create a Database Mail Profile](create-a-database-mail-profile.md).  
  
 Utilice los botones **Subir** y **Bajar** para cambiar el orden en que se utilizan las cuentas del Correo electrónico de base de datos. Este orden se determina mediante un valor denominado número de secuencia. El botón**Subir** reduce el número de secuencia y el botón **Bajar** aumenta el número de secuencia. El número de secuencia determina el orden en que el Correo electrónico de base de datos utiliza las cuentas en el perfil. En el caso de un mensaje de correo electrónico nuevo, el Correo electrónico de base de datos se inicia con la cuenta con el número de secuencia más bajo. Si la cuenta genera un error, el Correo electrónico de base de datos utiliza la cuenta con el siguiente número de secuencia superior y así sucesivamente hasta que el Correo electrónico de base de datos envía el mensaje correctamente o la cuenta con el número de secuencia superior genera un error. Si la cuenta con el número de secuencia superior genera un error, el Correo electrónico de base de datos pausa los intentos de envío del correo electrónico durante la cantidad de tiempo configurada en el parámetro **AccountRetryDelay** y, a continuación, inicia nuevamente el proceso de intento de envío del correo electrónico comenzando por el número de secuencia más bajo. Use el parámetro **AccountRetryAttempts** del Correo electrónico de base de datos para configurar el número de veces que el proceso de correo electrónico externo intenta enviar el mensaje de correo electrónico al usar cada cuenta del perfil especificado. Puede configurar los parámetros **AccountRetryDelay** y **AccountRetryAttempts** en la página **Configurar parámetros del sistema** del Asistente para configuración del Correo electrónico de base de datos.  
  
 **Nombre de perfil**  
 Permite seleccionar el nombre del perfil que se va a administrar.  
  
 **Eliminar**  
 Permite eliminar el perfil seleccionado. Se le pedirá que seleccione **Sí** para eliminar el perfil seleccionado y para no enviar los mensajes no enviados; o bien seleccione **No** para eliminar el perfil seleccionado solo si no existen mensajes sin enviar.  
  
 **Descripción**  
 Permite ver o cambiar la descripción del perfil seleccionado. La descripción es opcional.  
  
 **Cuentas SMTP**  
 Elija una o más cuentas para el perfil. La prioridad de conmutación por error establece el orden en que el Correo electrónico de base de datos utiliza la cuenta en caso de una conmutación por error.  
  
 **Add (Agregar)**  
 Agregue una cuenta al perfil.  
  
 **Remove**  
 Quite la cuenta seleccionada del perfil.  
  
 **Subir**  
 Permite aumentar la prioridad de conmutación por error de la cuenta seleccionada.  
  
 **Bajar**  
 Permite reducir la prioridad de conmutación por error de la cuenta seleccionada.  
  
 **Prioridad**  
 Permite ver la prioridad de conmutación por error actual de la cuenta.  
  
 **Nombre de cuenta**  
 Permite ver el nombre de la cuenta.  
  
 **Dirección de correo electrónico**  
 Permite ver la dirección de correo electrónico de la cuenta.  
  

  
###  <a name="add-account-to-profile-page"></a><a name="AddAccount"></a>Agregar cuenta a la página de perfil  
 Use esta página para elegir la cuenta que se va a agregar al perfil. Elija entre una cuenta existente en el cuadro **Nombre de cuenta** o haga clic en **Nueva cuenta**.  
  
 **Nombre de cuenta**  
 Seleccione el nombre de la cuenta que se va a agregar al perfil.  
  
 **Dirección de correo electrónico**  
 La dirección de correo electrónico de la cuenta seleccionada. No puede cambiar la dirección de correo electrónico en esta página. Para cambiar la dirección de correo electrónico de la cuenta, regrese a la página principal del asistente y seleccione la opción **Administrar cuentas y perfiles de Correo electrónico de base de datos** .  
  
 **Nombre del servidor**  
 El nombre del servidor de correo electrónico para la cuenta seleccionada. No puede cambiar el nombre del servidor en esta página. Para cambiar el nombre del servidor de la cuenta, regrese a la página principal del asistente y seleccione la opción **Administrar cuentas y perfiles de Correo electrónico de base de datos** .  
  
 **Nueva cuenta**  
 Crea una nueva cuenta.  
  

  
###  <a name="manage-accounts-and-profiles-page"></a><a name="AccountsProfiles"></a>Página administrar cuentas y perfiles  
 Utilice esta página para elegir una tarea para administrar un perfil o una cuenta.  
  
 **Creación de una nueva cuenta**  
 Crea una nueva cuenta.  
  
 **Ver, cambiar o eliminar cuenta existente**  
 Administra o elimina una cuenta existente.  
  
 **Crear nuevo perfil**  
 Crea un nuevo perfil.  
  
 **Ver, cambiar o eliminar un perfil existente. También puede administrar cuentas asociadas al perfil.**  
 Actualiza o elimina un perfil existente. Esta opción también le permite administrar cuentas asociadas al perfil.  
  

  
###  <a name="manage-profile-security-public-tab"></a><a name="ProfileSecurityPublic"></a>Administrar seguridad del perfil, pestaña público  
 Utilice esta página para configurar un perfil público.  
  
 Los perfiles son públicos o privados. Un perfil privado solo es accesible para determinados usuarios o roles. Un perfil público permite a cualquier usuario o rol con acceso a la base de datos host de correo (**msdb**) enviar correo electrónico al usar dicho perfil.  
  
 Los perfiles pueden ser predeterminados. En este caso, los usuarios o los roles pueden utilizar el perfil para enviar correo electrónico sin especificarlo explícitamente. Si el usuario o el rol que envía el mensaje de correo electrónico tiene un perfil privado predeterminado, el Correo electrónico de base de datos utilizará dicho perfil. Si el usuario o el rol no tiene un perfil privado predeterminado, **sp_send_dbmail** usa el perfil público predeterminado de la base de datos **msdb** . Si no hay ningún perfil privado predeterminado para el usuario o el rol ni tampoco ningún perfil público predeterminado para la base de datos, **sp_send_dbmail** devuelve un error. Solo se puede marcar un perfil como predeterminado.  
  
 **Pública**  
 Seleccione esta opción para convertir en público el perfil especificado.  
  
 **Nombre del perfil**  
 Muestra el nombre del perfil.  
  
 **Perfil predeterminado**  
 Seleccione esta opción para convertir en predeterminado el perfil especificado.  
  
 **Mostrar solo perfiles públicos existentes**  
 Seleccione esta opción para mostrar solo los perfiles públicos de la base de datos especificada.  
  

  
###  <a name="manage-profile-security-private-tab"></a><a name="ProfileSecurityPrivate"></a>Administrar seguridad del perfil, pestaña privado  
 Utilice esta página para configurar un perfil privado.  
  
 Los perfiles son públicos o privados. Un perfil privado solo es accesible para determinados usuarios o roles. Un perfil público permite a cualquier usuario o rol con acceso a la base de datos host de correo (**msdb**) enviar correo electrónico al usar dicho perfil.  
  
 Los perfiles pueden ser predeterminados. En este caso, los usuarios o los roles pueden utilizar el perfil para enviar correo electrónico sin especificarlo explícitamente. Si el usuario o el rol que envía el mensaje de correo electrónico tiene un perfil privado predeterminado, el Correo electrónico de base de datos utilizará dicho perfil. Si el usuario o el rol no tiene un perfil privado predeterminado, **sp_send_dbmail** usa el perfil público predeterminado de la base de datos **msdb** . Si no hay ningún perfil privado predeterminado para el usuario o el rol ni tampoco ningún perfil público predeterminado para la base de datos, **sp_send_dbmail** devuelve un error.  
  
 **Nombre de usuario**  
 Seleccione el nombre de un usuario o un rol de la base de datos **msdb** .  
  
 **Acceder**  
 Seleccione si el usuario o el rol tienen acceso al perfil especificado.  
  
 **Nombre de perfil**  
 Muestra el nombre del perfil.  
  
 **Es el perfil predeterminado**  
 Permite seleccionar si el perfil es el predeterminado para el usuario o el rol. Cada usuario o rol solo puede tener un perfil predeterminado  
  
 **Mostrar solo perfiles privados existentes para este usuario**  
 Seleccione esta opción para mostrar solo los perfiles a los que el usuario o el rol especificados ya tienen acceso.  
  

  
###  <a name="configure-system-parameters"></a><a name="SystemParameters"></a>Configurar parámetros del sistema  
 Utilice esta página para especificar los parámetros del sistema de Correo electrónico de base de datos. Visualice los parámetros del sistema y el valor actual de cada uno de ellos. Seleccione un parámetro para ver una descripción breve en el panel de información.  
  
 **Número de reintentos de cuenta**  
 Número de veces que el proceso de correo electrónico externo intenta enviar el mensaje de correo electrónico con cada cuenta del perfil especificado.  
  
 **Intervalo entre reintentos de cuenta (segundos)**  
 Cantidad de tiempo en segundos que el proceso de correo electrónico externo espera después de intentar entregar un mensaje con todas las cuentas del perfil antes de volver a intentarlo con todas las cuentas.  
  
 **Tamaño máximo del archivo (bytes)**  
 Tamaño máximo de los datos adjuntos en bytes.  
  
 **Extensiones de archivo adjunto prohibidas**  
 Lista de extensiones separadas por comas que no se puede enviar como datos adjuntos en un mensaje de correo electrónico. Haga clic en el botón Examinar (**...**) para agregar extensiones adicionales.  
  
 **Vigencia mínima del ejecutable de Correo electrónico de base de datos (segundos)**  
 Cantidad de tiempo mínima en segundos que el proceso de correo electrónico externo permanece activo. El proceso permanecerá activo mientras queden mensajes en la cola del Correo electrónico de base de datos. Este parámetro especifica el tiempo que permanece activo el proceso si no hay ningún mensaje por procesar.  
  
 **Nivel de registro**  
 Sirve para especificar qué mensajes se deben registrar en el registro de Correo electrónico de base de datos. Los valores posibles son:  
  
-   Normal: solo registra los errores  
  
-   Extendido: registra los errores, las advertencias y los mensajes informativos  
  
-   Detallado: registra errores, advertencias, mensajes informativos, mensajes de operación correcta y otros mensajes internos Utilice el registro detallado para la solución de problemas.  
  
 El valor predeterminado es Extendido.  
  
 **Restablecer todo**  
 Seleccione esta opción para restablecer los valores predeterminados de la página.  
  

  
###  <a name="complete-the-wizard-page"></a><a name="CompleteWizard"></a>Página finalización del asistente  
 Utilice esta página para revisar las acciones que realizará el **Asistente para configuración del Correo electrónico de base de datos** . Los cambios no se llevan a cabo hasta que finaliza el asistente.  
  

  
###  <a name="send-test-e-mail-page"></a><a name="TestEmail"></a>Página enviar correo electrónico de prueba  
 Use la página **Enviar correo electrónico de prueba desde**_<nombreDeInstancia>_ para enviar un mensaje de correo electrónico con el perfil de Correo electrónico de base de datos especificado. Los miembros del rol fijo de servidor **sysadmin** son los únicos que pueden enviar un mensaje de correo electrónico de prueba mediante esta página.  
  
 **Perfil de Correo electrónico de base de datos**  
 Seleccione un perfil de Correo electrónico de base de datos de la lista. Este campo es obligatorio. Si no aparece ningún perfil, significa que no hay ninguno o que no tiene permiso para ninguno. Utilice el **Asistente para configuración de Correo electrónico de base de datos** para crear y configurar perfiles. Si no aparece ningún perfil, utilice el Asistente para configuración de Correo electrónico de base de datos para crear un perfil para su utilización.  
  
 **To**  
 Dirección de correo electrónico de los destinatarios de los mensajes. Se requiere al menos un destinatario.  
  
 **Subject**  
 Línea de asunto del mensaje de correo electrónico de prueba. Cambie el asunto predeterminado a fin de identificar más fácilmente el mensaje para solucionar el problema.  
  
 **Cuerpo**  
 Cuerpo del mensaje de prueba. Cambie el asunto predeterminado a fin de identificar más fácilmente el mensaje para solucionar el problema.  
  
 En el cuadro de diálogo **Correo electrónico de prueba de base de datos** se confirma que el Correo electrónico de base de datos intentó enviar el mensaje de correo electrónico de prueba y se indica el **mailitem_id** del mismo. Pregunte al destinatario si ha recibido el mensaje. Normalmente, los mensajes de correo electrónico se reciben en pocos minutos, pero puede que se retrasen a causa de un rendimiento lento de la red, una acumulación de mensajes en el servidor de correo o si el servidor no está disponible temporalmente. Use **mailitem_id** para solucionar el problema.  
  
 **Correo electrónico enviado**  
 **mailitem_id** del mensaje de correo electrónico de prueba.  
  
 **Solución de problemas**  
 Haga clic para abrir los Libros en pantalla en el tema [Solucionar problemas del Correo electrónico de base de datos](https://msdn.microsoft.com/library/ms188663.aspx).  
  

  
##  <a name="using-templates"></a><a name="Template"></a>Uso de plantillas  
 **Para crear un script de configuración de Correo electrónico de base de datos**  
  
1.  En el menú **Ver** , seleccione **Explorador de plantillas**.  
  
2.  En la ventana **Explorador de plantillas** , expanda la carpeta **Correo electrónico de base de datos** .  
  
3.  Haga doble clic en **Simple Database Mail Configuration (Configuración de correo electrónico de base de datos simple)**. Se abre la plantilla en una ventana de consulta nueva.  
  
4.  En el menú **Consulta** , seleccione **Especificar valores para parámetros de plantilla**. Se abre la ventana **Reemplazar parámetros de plantilla** .  
  
5.  Escriba valores para **profile_name**, **account_name**, **SMTP_servername**, **email_address**y **display_name**. SQL Server Management Studio rellena la plantilla con los valores indicados.  
  
6.  Ejecute el script para crear la configuración.  
  
7.  El script no garantiza el acceso al perfil para los usuarios de la base de datos. Por lo tanto, de forma predeterminada, solo pueden utilizar el perfil los miembros del rol fijo de seguridad **sysadmin** . Para obtener más información sobre cómo conceder acceso a los perfiles, vea [sysmail_add_principalprofile_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-add-principalprofile-sp-transact-sql).  
  
  
