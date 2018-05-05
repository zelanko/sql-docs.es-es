---
title: El controlador ODBC para Oracle | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a129bbc39f35c2418fc0dc5d34e534d4c7fb8cbc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="odbc-driver-for-oracle"></a>Controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Microsoft® ODBC Driver for Oracle permite conectar su aplicación compatible con ODBC con una base de datos de Oracle. El controlador ODBC para Oracle se ajusta a la especificación de Open Database Connectivity (ODBC) que se describe en el *referencia del programador de ODBC*. Permitir el acceso a paquetes de PL/SQL, la integración de XA/DTC y acceso de Oracle desde dentro de Internet Information Services (IIS).  
  
 Oracle RDBMS es un sistema de administración de base de datos relacional multiusuario que se ejecute con distintos sistemas operativos minicomputadoras y de estación de trabajo. Equipos compatibles con IBM que ejecutan Microsoft Windows pueden comunicarse con servidores de base de datos de Oracle a través de una red. Redes compatibles incluyen Microsoft LAN Manager, NetWare, VINES, DECnet y cualquier red que admita TCP/IP.  
  
 El controlador ODBC para Oracle permite que una aplicación tener acceso a datos en una base de datos de Oracle a través de la interfaz ODBC. El controlador puede tener acceso a bases de datos de Oracle locales o se puede comunicar con la red a través de SQL * Net. En el diagrama siguiente se detalla esta arquitectura de aplicaciones y controladores.  
  
 ![El controlador ODBC para Oracle aplicación&#47;arquitectura de controladores](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 El controlador ODBC para Oracle es compatible con la API de conformidad de nivel 1 y principal de nivel de conformidad de SQL. También admite algunas funciones de API de conformidad de nivel 2 y la mayoría de la gramática de los niveles de conformidad principal y extendida de SQL. El controlador es compatible con 2.5 de ODBC y es compatible con sistemas de 32 bits. Oracle 7.3 x se admite totalmente; Oracle8 tiene compatibilidad limitada. El controlador ODBC para Oracle no admite cualquiera de los nuevos tipos de datos de Oracle8: tipos de datos Unicode, BLOB, CLOB, y así sucesivamente, ni tampoco admite el nuevo modelo de objetos relacionales de Oracle. Para obtener más información acerca de los tipos de datos admitidos, consulte [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) en esta guía.  
  
 Para obtener acceso a datos de Oracle, se requieren los siguientes componentes:  
  
-   El controlador ODBC para Oracle  
  
-   Una base de datos de Oracle RDBMS  
  
-   Software de cliente de Oracle  
  
 Además, para las conexiones remotas:  
  
-   Una red que conecta a los equipos que ejecutan el controlador y la base de datos. La red debe admitir SQL * Net conexiones.  
  
## <a name="component-documentation"></a>Documentación de componente  
 Esta guía contiene información detallada sobre la configuración y configurar el controlador ODBC de Microsoft para Oracle y agregar la funcionalidad de programación. También contiene material de referencia técnica.  
  
 Para obtener información sobre el comportamiento específico del producto de Oracle, consulte la documentación que acompaña a los productos de Oracle.  
  
 Para obtener información acerca de la instalación y configuración de Microsoft ODBC Driver for Oracle se realiza mediante el Administrador de orígenes de datos ODBC, vea el [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) documentación.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El controlador ODBC para Oracle usuario ' guía](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [El controlador ODBC para Oracle programador ' s referencia](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
