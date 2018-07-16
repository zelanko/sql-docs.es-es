---
title: Crear base de datos (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.createdatabase.f1
ms.assetid: 56a8a79f-086c-4bdc-8888-0045bb4b0cbf
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 472daf928c92c69ab330ae1d77e6a6021c96e04f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250495"
---
# <a name="create-database-sql-server-import-and-export-wizard"></a>Crear base de datos (Asistente para importación y exportación de SQL Server)
  Use la **Create Database** página para definir una nueva base de datos para un archivo de destino.  
  
 Esta página ofrece un subconjunto de las opciones disponibles para crear una nueva base de datos. Para ver todas las opciones, use [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 Para más información acerca de este asistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Proporcione un nombre único para la base de datos de SQL Server de destino. Cuando asigne un nombre a esta base de datos, asegúrese de respetar las convenciones de SQL Server.  
  
 **Nombre de archivo de datos**  
 Muestra el nombre del archivo de datos. Éste proviene del nombre de la base de datos que proporcionó anteriormente.  
  
 **Nombre de archivo de registro**  
 Muestra el nombre del archivo de registro. Éste proviene del nombre de la base de datos que proporcionó anteriormente.  
  
 **Tamaño inicial (archivo de datos)**  
 Especifique el número de megabytes para el tamaño inicial del archivo de datos.  
  
 **No se permite el crecimiento (archivo de datos)**  
 Indique si el archivo de datos puede aumentar de tamaño más allá del tamaño inicial especificado.  
  
 **Crecimiento por porcentaje (archivo de datos)**  
 Especifique un porcentaje por el cual el archivo de datos puede aumentar de tamaño.  
  
 **Crecimiento por tamaño (archivo de datos)**  
 Especifique un número de megabytes por el cual el archivo de datos puede aumentar de tamaño.  
  
 **Tamaño inicial (archivo de registro)**  
 Especifique el número de megabytes para el tamaño inicial del archivo de registro.  
  
 **No se permite el crecimiento (archivo de registro)**  
 Indique si el archivo de registro puede aumentar de tamaño, más allá del tamaño inicial especificado.  
  
 **Crecimiento por porcentaje (archivo de registro)**  
 Especifique un porcentaje por el cual el archivo de registro puede aumentar de tamaño.  
  
 **Crecimiento por tamaño (archivo de registro)**  
 Especifique un número de megabytes por el cual el archivo de registro puede aumentar de tamaño.  
  
  
