---
title: Seguridad del Agente de distribución | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.rep.security.DA.f1
helpviewer_keywords:
- Distribution Agent Security dialog box
ms.assetid: de40cc21-2e58-4464-9be7-b5b90c925e9b
caps.latest.revision: 25
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3dd07937e02644043078dd82c98e14143b6ae241
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="distribution-agent-security"></a>Seguridad del Agente de distribución
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El cuadro de diálogo **Seguridad del Agente de distribución** permite especificar la cuenta de Windows con la que se ejecuta el Agente de distribución. El Agente de distribución se ejecuta en el distribuidor para las suscripciones de inserción y en el suscriptor para las suscripciones de extracción. La cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows se denomina también *cuenta de proceso*porque el proceso del agente se ejecuta con dicha cuenta. Las opciones adicionales disponibles en el cuadro de diálogo dependen de cómo se tenga acceso al mismo:  
  
-   Si se tiene acceso al cuadro de diálogo desde el Asistente para nueva suscripción, es posible especificar también el contexto en que el Agente de distribución realiza conexiones al suscriptor (para las suscripciones de inserción) o al distribuidor (para las suscripciones de extracción). La conexión se puede realizar suplantando la cuenta de Windows o en el contexto de la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se especifique.  
  
-   Si se tiene acceso al cuadro de diálogo desde el cuadro de diálogo **Propiedades de la suscripción** , especifique el contexto en que el Agente de distribución realiza las conexiones haciendo clic en el botón de propiedades (**...**) de la fila **Conexión de suscriptor** o **Conexión del distribuidor** de ese cuadro de diálogo. Para más información sobre cómo acceder al cuadro de diálogo **Propiedades de suscripción**, vea [Ver y modificar las propiedades de una suscripción de inserción](../../relational-databases/replication/view-and-modify-push-subscription-properties.md) y [Ver y modificar las propiedades de una suscripción de extracción](../../relational-databases/replication/view-and-modify-pull-subscription-properties.md).  
  
 Todas las cuentas deben ser válidas y se debe especificar la contraseña correcta para cada cuenta. Las cuentas y las contraseñas se validan cuando se ejecuta el agente.  
  
## <a name="options"></a>Opciones  
 **Process Account**  
 Indique la cuenta de Windows con la que se ejecuta el Agente de distribución:  
  
-   Para las suscripciones de inserción, la cuenta debe:  
  
    -   Ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de distribución.  
  
    -   Ser miembro de la lista de acceso a la publicación (PAL).  
  
    -   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
    -   Tener permisos de lectura en el directorio de instalación del proveedor OLE DB para el suscriptor si la suscripción es para un suscriptor que no sea de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para las suscripciones de extracción, la cuenta debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
 Si se suplanta la cuenta de proceso al realizar las conexiones serán necesarios permisos adicionales. Vea las secciones **Conectar al distribuidor** y **Conectar al suscriptor** a continuación.  
  
 No se puede especificar la**Cuenta de proceso** para las suscripciones de extracción a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]porque el Agente de distribución no se ejecuta en instancias de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
 **Contraseña** y **Confirmar contraseña**  
 Escriba la contraseña de la cuenta de Windows.  
  
 **Conectar al distribuidor**  
 Para las suscripciones de inserción, las conexiones al distribuidor se realizan siempre suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de extracción, seleccione si el Agente de distribución debe realizar conexiones al distribuidor suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** o utilizando una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión debe:  
  
-   Ser miembro de la PAL.  
  
-   Tener permisos de lectura en el recurso compartido de instantáneas.  
  
 **Conectar al suscriptor**  
 Para las suscripciones de extracción, las conexiones con el suscriptor siempre se realizan suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** .  
  
 Para las suscripciones de inserción, las opciones para los suscriptores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y para los suscriptores que no sean de-[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son diferentes:  
  
-   Para los suscriptores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : seleccione si el Agente de distribución debe realizar conexiones al suscriptor suplantando la cuenta especificada en el cuadro de texto **Cuenta de proceso** o utilizando una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si selecciona utilizar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique una contraseña y un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    > [!NOTE]  
    >  Se recomienda usar la suplantación de la cuenta de Windows en lugar de usar una cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     La cuenta de Windows o la cuenta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usada para la conexión con el suscriptor debe ser como mínimo miembro del rol fijo de base de datos **db_owner** en la base de datos de suscripciones.  
  
-   Para los suscriptores que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especifique el inicio de sesión de la base de datos del suscriptor que se utilizará cuando el Agente de distribución se conecte al suscriptor. Este inicio de sesión debe disponer de los permisos suficientes para crear objetos en la base de datos de suscripciones. Para más información sobre la configuración de suscriptores no son de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Crear una suscripción para un suscriptor que no sea de SQL Server](../../relational-databases/replication/create-a-subscription-for-a-non-sql-server-subscriber.md).  
  
 **Opciones de conexión adicionales**  
 Solo para suscriptores que no sean de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Especifique cualquier opción de conexión para el suscriptor en forma de cadena de conexión (Oracle no requiere opciones adicionales). Las opciones deben ir separadas con punto y coma. A continuación se ofrece un ejemplo de una cadena de conexión de IBM DB2 (se han incluido saltos de línea para facilitar la lectura):  
  
```  
Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
Persist Security Info=False;Connection Pooling=True;  
```  
  
 La mayoría de las opciones de la cadena son específicas para el servidor DB2 que está configurando, pero la opción **Process Binary as Character** siempre debe establecerse en **False**. Se requiere un valor para que la opción **Catálogo original** identifique la base de datos de suscripciones. Para más información, consulte [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md).  
  
## <a name="see-also"></a>Ver también  
 [Administrar inicios de sesión y contraseñas en la replicación](../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [Modelo de seguridad del Agente de replicación](../../relational-databases/replication/security/replication-agent-security-model.md)   
 [Replication Agents Overview](../../relational-databases/replication/agents/replication-agents-overview.md)  (Información general sobre los agentes de replicación)  
 [Replication Security Best Practices](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Suscribirse a publicaciones](../../relational-databases/replication/subscribe-to-publications.md)  
  
  
