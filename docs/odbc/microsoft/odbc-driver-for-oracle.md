---
title: Controlador ODBC para Oracle ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298135"
---
# <a name="odbc-driver-for-oracle"></a>Controlador ODBC para Oracle
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 El controlador ODBC ® Microsoft para Oracle le permite conectar la aplicación compatible con ODBC a una base de datos de Oracle. El controlador ODBC para Oracle se ajusta a la especificación de conectividad de base de datos abierta (ODBC) descrita en la *referencia del programador ODBC*. Permite el acceso a paquetes PL/SQL, integración XA/DTC y acceso de Oracle desde Internet Information Services (IIS).  
  
 Oracle RDBMS es un sistema de gestión de bases de datos relacionales multiusuario que se ejecuta con varios sistemas operativos de estaciones de trabajo y miniordenadores. Los equipos compatibles con IBM que ejecutan Microsoft Windows pueden comunicarse con los servidores de bases de datos Oracle a través de una red. Las redes compatibles incluyen Microsoft LAN Manager, NetWare, VINES, DECnet y cualquier red que admita TCP/IP.  
  
 El controlador ODBC para Oracle permite que una aplicación tenga acceso a los datos de una base de datos de Oracle a través de la interfaz ODBC. El controlador puede acceder a bases de datos locales de Oracle o puede comunicarse con la red a través de SQL*Net. En el diagrama siguiente se detalla esta arquitectura de aplicación y controlador.  
  
 ![Controlador ODBC para la arquitectura del controlador de&#47;de aplicaciones de Oracle](../../odbc/microsoft/media/orcdrvsdkarch.gif "OrcDrvSDKArch")  
  
 El controlador ODBC para Oracle cumple con API Conformance Level 1 y SQL Conformance Level Core. También admite algunas funciones en API Conformance Level 2 y la mayor parte de la gramática en los niveles de conformidad Core y Extended SQL. El controlador es compatible con ODBC 2.5 y admite sistemas de 32 bits. Oracle 7.3x es compatible completamente; Oracle8 tiene soporte limitado. El controlador ODBC para Oracle no admite ninguno de los nuevos tipos de datos de Oracle8 (tipos de datos Unicode, BLLOB, CLOB, etc.- ni admite el nuevo modelo de objetos relacionales de Oracle. Para obtener más información acerca de los tipos de datos admitidos, consulte Tipos de [datos admitidos](../../odbc/microsoft/supported-data-types-odbc-driver-for-oracle.md) en esta guía.  
  
 Para acceder a los datos de Oracle, se requieren los siguientes componentes:  
  
-   El controlador ODBC para Oracle  
  
-   Una base de datos Oracle RDBMS  
  
-   Oracle Client Software  
  
 Además, para conexiones remotas:  
  
-   Una red que conecta los equipos que ejecutan el controlador y la base de datos. La red debe admitir conexiones SQL*Net.  
  
## <a name="component-documentation"></a>Documentación de componentes  
 Esta guía contiene información detallada sobre cómo configurar y configurar el controlador ODBC de Microsoft para Oracle y agregar funcionalidad mediante programación. También contiene material de referencia técnica.  
  
 Para obtener información sobre el comportamiento específico de los productos de Oracle, consulte la documentación que acompaña al producto Oracle.  
  
 Para obtener información acerca de cómo configurar o configurar el controlador ODBC de Microsoft para Oracle mediante el Administrador de orígenes de datos ODBC, consulte la documentación del Administrador de orígenes de [datos ODBC.](../../odbc/admin/odbc-data-source-administrator.md)  
  
 Esta sección contiene los temas siguientes.  
  
-   [El controlador ODBC para Oracle usuario ' guía](../../odbc/microsoft/odbc-driver-for-oracle-user-s-guide.md)  
  
-   [El controlador ODBC para Oracle programador ' s referencia](../../odbc/microsoft/odbc-driver-for-oracle-programmer-s-reference.md)
