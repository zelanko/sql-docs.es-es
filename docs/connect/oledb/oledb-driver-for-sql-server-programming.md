---
title: Controlador OLE DB para la programación de SQL Server | Documentos de Microsoft
description: Controlador de OLE DB para la programación de SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 1a3d642eb3cef1f9f01accd8b50f571f5e4903ac
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server-programming"></a>Controlador OLE DB para la programación de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Controlador de OLE DB para SQL Server es una datos independiente acceso aplicación interfaz de programación (API) utilizada para OLE DB, que se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Controlador de OLE DB para SQL Server ofrece al controlador OLE DB de SQL en una biblioteca de vínculos dinámicos (DLL). También ofrece muchas más funciones nuevas de las que se proporcionaban en Data Access Components para Windows (DAC para Windows, anteriormente Microsoft Data Access Components o MDAC). Controlador de OLE DB para SQL Server puede utilizarse para crear nuevas aplicaciones o mejorar las aplicaciones existentes que necesitan aprovechar las características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], por ejemplo, varios conjuntos de resultados activos (MARS), tipos de datos definidos por el usuario (UDT), consulta admiten notificaciones, el aislamiento de instantánea y el tipo de datos XML.  
  
> [!NOTE]  
>  Para obtener una lista de las diferencias entre el controlador OLE DB para SQL Server y Windows DAC, además de información sobre los problemas a tener en cuenta antes de actualizar una aplicación de Windows DAC al controlador de OLE DB para SQL Server, vea [actualizar una aplicación a controlador de OLE DB de SQL Servidor de MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 El controlador OLE DB para SQL Server puede utilizarse junto con OLE DB Core servicios suministrados con DAC para Windows, pero esto no es un requisito; la opción de usar los servicios principales o no depende de los requisitos de la aplicación individual (por ejemplo, si se requiere la agrupación de conexiones).  
  
 Las aplicaciones de objeto de datos ActiveX (ADO) pueden usar el controlador OLE DB para SQL Server, pero se recomienda usar ADO junto con el **DataTypeCompatibility** palabra clave de cadena de conexión (o el correspondiente  **Origen de datos** propiedad). Cuando se usa el controlador OLE DB para SQL Server, las aplicaciones ADO pueden aprovecharse de las nuevas características introducidas en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] que están disponibles mediante el controlador OLE DB para SQL Server a través de palabras clave de cadena de conexión o propiedades de OLE DB o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Para obtener más información sobre el uso de estas características con ADO, vea [utilizar ADO con el controlador OLE DB para SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 Controlador de OLE DB para SQL Server se diseñó para proporcionar un método simplificado de obtener acceso a datos nativos a SQL Server mediante OLE DB. Proporciona una manera innovar y desarrollar nuevas características de acceso de datos sin tener que cambiar los componentes de Windows DAC actuales, que forman parte de la plataforma Microsoft Windows.  
  
 Mientras el controlador OLE DB para SQL Server utiliza componentes de DAC para Windows, no es explícitamente depende de una versión concreta de DAC para Windows. Puede usar el controlador OLE DB para SQL Server con la versión de DAC para Windows que se instala con cualquier sistema operativo compatible con el controlador OLE DB para SQL Server.  
  
## <a name="in-this-section"></a>En esta sección  
 [Controlador OLE DB para SQL Server](../oledb/oledb-driver-for-sql-server.md)  
 Enumera el significativo nuevo controlador OLE DB para características de SQL Server.  
  
 [Cuándo se debe utilizar el controlador OLE DB para SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Describe cómo controlador OLE DB para SQL Server se ajusta con datos de Microsoft tecnologías de acceso, ¿cómo se compara con DAC para Windows y ADO.NET y proporciona punteros para decidir qué tecnología de acceso a datos.  
  
 [Controlador OLE DB para características de SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Describe las características admitidas por el controlador OLE DB para SQL Server.  
  
 [Generar aplicaciones con el controlador OLE DB para SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Proporciona información general del controlador de OLE DB para el desarrollo de SQL Server, incluido cómo difiere de la DAC para Windows, los componentes que utiliza, y cómo puede usar ADO con él.  
  
 Esta sección también trata el controlador OLE DB para la instalación de SQL Server y la implementación, incluida la forma de redistribuir el controlador OLE DB para la biblioteca de SQL Server.  
  
 [Requisitos del sistema para el controlador OLE DB para SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Describe los recursos del sistema necesarios para usar el controlador OLE DB para SQL Server.  
  
 [Controlador OLE DB para SQL Server &#40;OLE DB&#41;](../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)  
 Proporciona información sobre cómo usar el controlador OLE DB para SQL Server.  
  
 [Buscar más OLE DB controlador para información sobre SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Proporciona recursos adicionales sobre el controlador OLE DB para SQL Server, incluidos los vínculos a recursos externos y obtención de más ayuda.  
  
  
## <a name="see-also"></a>Vea también  
 [Actualizar una aplicación de SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Temas "Cómo..." de OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
