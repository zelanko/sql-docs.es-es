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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 093cb7352a7f509b0afcc061e2691311bb183169
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298135"
---
# <a name="odbc-driver-for-oracle"></a>Controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC de Microsoft® para Oracle le permite conectar su aplicación compatible con ODBC a una base de datos de Oracle. El controlador ODBC para Oracle se ajusta a la especificación de conectividad abierta de bases de datos (ODBC) que se describe en la *Referencia del programador de ODBC*. Permite el acceso a paquetes PL/SQL, la integración de XA/DTC y el acceso a Oracle desde Internet Information Services (IIS).  
  
 RDBMS de Oracle es un sistema de administración de bases de datos relacionales multiusuario que se ejecuta con varios sistemas operativos de estación de trabajo y minicomputer. Los equipos compatibles con IBM que ejecutan Microsoft Windows pueden comunicarse con los servidores de bases de datos de Oracle a través de una red. Entre las redes admitidas se incluyen Microsoft LAN Manager, NetWare, VINEs, DECnet y cualquier red que admita TCP/IP.  
  
 El controlador ODBC para Oracle permite a una aplicación tener acceso a los datos de una base de datos de Oracle a través de la interfaz ODBC. El controlador puede tener acceso a bases de datos de Oracle locales o puede comunicarse con la red a través de SQL * Net. En el siguiente diagrama se detalla esta arquitectura de aplicaciones y controladores.  
  
 ![Arquitectura de controladores ODBC para el controlador de&#47;de aplicaciones Oracle](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 El controlador ODBC para Oracle cumple con el nivel de conformidad de API 1 y el nivel de cumplimiento de SQL básico. También admite algunas funciones en el nivel de cumplimiento de API 2 y la mayor parte de la gramática en los niveles de cumplimiento básico y extendido de SQL. El controlador es compatible con ODBC 2,5 y admite sistemas de 32 bits. Oracle 7.3 x es totalmente compatible; Oracle8 tiene compatibilidad limitada. El controlador ODBC para Oracle no es compatible con ninguno de los nuevos tipos de datos Oracle8-tipos de datos Unicode, blobs, CLOB, etc., ni tampoco admite el nuevo modelo de objetos relacionales de Oracle. Para obtener más información sobre los tipos de datos admitidos, vea [tipos de datos admitidos](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) en esta guía.  
  
 Para tener acceso a los datos de Oracle, se necesitan los siguientes componentes:  
  
-   El controlador ODBC para Oracle  
  
-   Una base de datos RDBMS de Oracle  
  
-   Software cliente de Oracle  
  
 Además, para las conexiones remotas:  
  
-   Una red que conecta los equipos que ejecutan el controlador y la base de datos. La red debe ser compatible con las conexiones de SQL * Net.  
  
## <a name="component-documentation"></a>Documentación de componentes  
 Esta guía contiene información detallada acerca de la instalación y configuración de Microsoft ODBC driver for Oracle y la incorporación de la funcionalidad de programación. También contiene material de referencia técnica.  
  
 Para obtener información sobre el comportamiento específico del producto de Oracle, consulte la documentación que acompaña al producto de Oracle.  
  
 Para obtener información acerca de cómo instalar o configurar el controlador ODBC de Microsoft para Oracle mediante el administrador de orígenes de datos ODBC, vea la documentación del [Administrador de orígenes de datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) .  
  
 Esta sección contiene los temas siguientes.  
  
-   [El controlador ODBC para Oracle usuario ' guía](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [El controlador ODBC para Oracle programador ' s referencia](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
