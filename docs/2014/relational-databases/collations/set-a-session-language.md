---
title: Establecer un idioma de la sesión | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
author: stevestein
ms.author: sstein
ms.openlocfilehash: da8d6adce66ac5b97e533b5afaefabda40e4b966
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953453"
---
# <a name="set-a-session-language"></a>Establecer un idioma de la sesión
  El idioma de la sesión se puede utilizar para establecer la forma en que se muestran los siguientes elementos en el servidor, dependiendo de la preferencia cultural y de idioma:  
  
-   El lenguaje que se usará para los mensajes de error y otros mensajes del sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varias copias de todas las cadenas de error del sistema y mensajes en todos los idiomas en los que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible. Estos mensajes se pueden ver en la vista de catálogo [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) . Cuando se instala una versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], estos mensajes del sistema se traducen a la versión de idioma que se instala. También se obtiene de forma predeterminada. El conjunto en inglés de EE.UU. de estos mensajes Además, se pueden agregar mensajes definidos por el usuario en un idioma específico con [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql).  
  
-   El formato de los datos de fecha y hora.  
  
-   Los nombres de días y meses, incluidas las abreviaturas.  
  
-   El primer día de la semana.  
  
-   Los datos de moneda.  
  
 Existen 33 idiomas disponibles para ser utilizados como valores de la sesión. Para obtener una lista de los idiomas, vea [sys.syslanguages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql).  
  
## <a name="setting-the-session-language-from-the-server"></a>Configurar el idioma de la sesión desde el servidor  
 Para establecer el idioma de la sesión desde el servidor, utilice [SET LANGUAGE](/sql/t-sql/statements/set-language-transact-sql).  
  
## <a name="setting-the-session-language-from-the-client"></a>Configurar el idioma de la sesión desde el cliente  
 El idioma de la sesión se puede establecer del lado cliente con OLE DB, ODBC o ADO.NET. Para OLE DB, utilice la propiedad SSPROP_INIT_CURRENTLANGUAGE. Para obtener más información, vea [Propiedades de inicialización y autorización](../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Para ODBC, utilice la palabra clave Language. Para más información, consulte [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md).  
  
 Para ADO.NET, utilice el parámetro **Current Language** del objeto **ConnectionString** . Para obtener más información, vea la documentación del kit de desarrollo de software (SDK) de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC).  
  
  
