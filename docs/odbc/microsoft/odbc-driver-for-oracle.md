---
title: Controlador ODBC para Oracle | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC]
- ODBC driver for Oracle [ODBC], about ODBC driver for Oracle
- Oracle data access [ODBC]
ms.assetid: 937e0662-8b1d-44f7-b077-4015c6605b2c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4685d209d768bd3ff41c1c7367ef6cb6dcd45bcf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63043870"
---
# <a name="odbc-driver-for-oracle"></a>Controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Microsoft® ODBC Driver for Oracle permite conectar su aplicación compatible con ODBC a una base de datos de Oracle. El controlador ODBC para Oracle se ajusta a la especificación de Open Database Connectivity (ODBC) se describe en el *referencia del programador de ODBC*. Permite el acceso a los paquetes de PL/SQL, integración de XA/DTC y acceso de Oracle desde dentro de Internet Information Services (IIS).  
  
 Oracle RDBMS es un sistema de administración de varios usuarios de base de datos relacional que se ejecute con distintos sistemas operativos de estación de trabajo y minicomputadoras. Equipos compatibles con IBM Microsoft Windows pueden comunicarse con servidores de base de datos de Oracle a través de una red. Redes admitidas incluyen Microsoft LAN Manager, NetWare, VINES, DECnet y cualquier red que es compatible con TCP/IP.  
  
 El controlador ODBC para Oracle permite que una aplicación tener acceso a datos en una base de datos de Oracle a través de la interfaz ODBC. El controlador puede tener acceso a bases de datos de Oracle locales o se puede comunicar con la red a través de SQL * Net. El siguiente diagrama ilustra esta arquitectura de aplicaciones y controladores.  
  
 ![Controlador ODBC para Oracle aplicación&#47;arquitectura de controladores](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 El controlador ODBC para Oracle cumple con API de conformidad de nivel 1 y principales del nivel de conformidad de SQL. También admite algunas funciones en 2 de nivel de conformidad de API y la mayoría de la gramática de los niveles de conformidad de Core y SQL extendido. El controlador es compatible con 2.5 de ODBC y es compatible con sistemas de 32 bits. Oracle 7.3 x se admite por completo; Oracle8 tiene compatibilidad limitada. El controlador ODBC para Oracle no admite cualquiera de los tipos de datos de Oracle8 - los tipos de datos Unicode, BLOB, CLOB y así sucesivamente - ni admite nuevo modelo de objetos relacionales de Oracle. Para obtener más información acerca de los tipos de datos admitidos, consulte [Supported Data Types](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) en esta guía.  
  
 Para obtener acceso a datos de Oracle, se requieren los siguientes componentes:  
  
-   El controlador ODBC para Oracle  
  
-   Una base de datos de RDBMS de Oracle  
  
-   Software cliente de Oracle  
  
 Además, para las conexiones remotas:  
  
-   Una red que conecta los equipos que ejecutan el controlador y la base de datos. La red debe ser compatible con SQL * Net conexiones.  
  
## <a name="component-documentation"></a>Documentación del componente  
 Esta guía contiene información detallada sobre cómo instalar y configurar el controlador ODBC de Microsoft para Oracle y agregar funcionalidad mediante programación. También contiene material de referencia técnica.  
  
 Para obtener información sobre el comportamiento específico del producto de Oracle, consulte la documentación que acompaña a los productos de Oracle.  
  
 Para obtener información sobre cómo instalar o configurar el controlador ODBC de Microsoft para Oracle mediante el Administrador de orígenes de datos ODBC, vea el [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) documentación.  
  
 Esta sección contiene los temas siguientes.  
  
-   [El controlador ODBC para Oracle usuario ' guía](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [El controlador ODBC para Oracle programador ' s referencia](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
