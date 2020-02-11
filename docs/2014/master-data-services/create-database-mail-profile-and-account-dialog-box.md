---
title: Cuadro de diálogo Crear perfil y cuenta de Correo electrónico de base de datos (Administrador de configuración de Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
f1_keywords:
- sql12.mds.configmanager.dbmailprofileacct.f1
ms.assetid: b93ea3d4-9f22-490e-8e26-d766b454aed6
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: b614422d3670dc30e0714b18bbf42ed87f1886af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65483276"
---
# <a name="create-database-mail-profile-and-account-dialog-box-master-data-services-configuration-manager"></a>Cuadro de diálogo Crear un perfil y una cuenta de Correo electrónico de base datos (Administrador de configuración de Master Data Services)
  Utilice el cuadro de diálogo **Crear un perfil y una cuenta de Correo electrónico de base de datos** para crear un perfil de Correo electrónico de base de datos y una cuenta de Correo electrónico de base de datos para la base de datos [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Este perfil se utilizará para notificar por correo electrónico a usuarios y grupos cuando se produzcan errores en la validación de una regla de negocios.  
  
## <a name="database-mail-profile-and-account"></a>Perfil y cuenta de Correo electrónico de base de datos  
 Un *Perfil de Correo electrónico de base de datos* es una colección de cuentas de Correo electrónico de base de datos. Una *cuenta de correo electrónico de base de datos* contiene la información [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que utiliza para enviar mensajes de correo electrónico a un servidor SMTP. Cuando crea el perfil y la cuenta en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)], la cuenta se agrega automáticamente al perfil y la información de esa cuenta se utiliza para enviar correos electrónicos.  
  
> [!NOTE]  
>  No puede utilizar [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] para actualizar los perfiles o cuentas de Correo electrónico de base de datos existentes ni puede configurar más de una cuenta para un perfil. Para realizar más tareas avanzadas con el Correo electrónico de base de datos, puede usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o scripts Transact-SQL. Para obtener más información, vea la sección [Database Mail Configuration Objects](../relational-databases/database-mail/database-mail-configuration-objects.md) en los Libros en pantalla de SQL Server.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Nombre del perfil**|Especifique un nombre para el nuevo perfil de Correo electrónico de base de datos. Este nombre debe ser único en los perfiles del Correo electrónico de base de datos configurados para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] .<br /><br /> Después de crear este perfil, estará disponible y seleccionado en la página **Base de datos** en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)].|  
|**Nombre de cuenta**|Escriba un nombre para la nueva cuenta de Correo electrónico de base de datos que se utilizará cuando se asocie a este perfil. Este nombre debe ser único en las cuentas de Correo electrónico de base de datos configurados para la base de datos de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] . Esta cuenta no se corresponde con una cuenta de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ni con una cuenta de usuario de Windows.|  
  
## <a name="outgoing-smtp-mail-server"></a>Servidor de correo saliente (SMTP)  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Dirección de correo electrónico**|Escriba el nombre de la dirección de correo electrónico de la cuenta. Esta es la dirección de correo electrónico desde la que se envía el correo electrónico y debe tener el formato *email_name*@*domain_name*. Un ejemplo de dirección de correo electrónico sería sales@contoso.com.|  
|**Nombre para mostrar**|Valor opcional. Escriba el nombre para mostrar en los mensajes de correo electrónico enviados desde esta cuenta. Un ejemplo de nombre para mostrar es Grupo de ventas Contoso.|  
|**Dirección de correo electrónico de respuesta**|Valor opcional. Escriba la dirección de correo electrónico que se utilizará para las respuestas a los mensajes enviados desde esta cuenta. Un ejemplo de dirección de correo electrónico de respuesta sería admin@contoso.com.|  
|**Servidor SMTP**|Escriba el nombre o la dirección IP del servidor SMTP que utiliza la cuenta para enviar correo electrónico. `smtp.` *<>* `.com`COMPANY_NAME un formato de servidor SMTP de ejemplo. Si necesita ayuda, consulte a su administrador de correo.|  
|**Número de Puerto**|Escriba el número de puerto del servidor SMTP de esta cuenta. El número de puerto SMTP es 25.|  
|**Este servidor requiere una conexión segura (SSL)**|Cifra la comunicación mediante SSL (Capa de sockets seguros).|  
  
## <a name="smtp-authentication"></a>Autenticación SMTP  
 El Correo electrónico de base de datos se puede enviar mediante las credenciales de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)], mediante otras credenciales que suministre o de forma anónima. Si su servidor de correo electrónico requiere autenticación, se recomienda crear una cuenta de usuario para su uso con Correo electrónico de base de datos. Esta cuenta de usuario debe tener permisos mínimos y no debe usarse para otros fines.  
  
|Nombre del control|Descripción|  
|------------------|-----------------|  
|**Autenticación de Windows con credenciales de servicio de Motor de base de datos**|Especifique que correo electrónico de base de datos deben utilizar las credenciales de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] la cuenta de servicio de Windows para la autenticación en el servidor SMTP.|  
|**Autenticación básica**|Especifique que Correo electrónico de base de datos debería utilizar un nombre de usuario y contraseña concretos para la autenticación en el servidor SMTP. Esta información solo se utiliza para la autenticación con el servidor de correo electrónico y no es necesario que la cuenta se corresponda con un usuario de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o con un usuario del equipo que ejecuta [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|  
|**Nombre de usuario**|Escriba el nombre de la cuenta de usuario que utiliza Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, es necesario un nombre de usuario.|  
|**Contraseña**|Escriba la contraseña que utiliza el Correo electrónico de base de datos para iniciar la sesión en el servidor SMTP. Si el servidor SMTP requiere autenticación básica, es necesaria una contraseña.|  
|**Confirmar contraseña**|Escriba de nuevo la contraseña para confirmarla.|  
|**Autenticación anónima**|Especifique que el servidor SMTP no requiere autenticación. Correo electrónico de base de datos no utilizará ninguna credencial para la autenticación en el servidor SMTP.|  
  
## <a name="see-also"></a>Consulte también  
 [Página configuración de base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../2014/master-data-services/database-configuration-page-master-data-services-configuration-manager.md)   
 [Configurar la base de datos y el sitio web para Master Data Services](set-up-the-database-and-website-for-master-data-services.md)  
  
  
