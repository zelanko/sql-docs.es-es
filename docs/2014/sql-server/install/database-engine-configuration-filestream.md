---
title: 'Filestream: configuración del motor de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], about FILESTREAM
ms.assetid: 641a10a1-ae52-4d26-8f1c-a032a4aeff02
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aa6f1df8858f5ba9bf302eb6a415182cfa9442c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095790"
---
# <a name="database-engine-configuration---filestream"></a>Configuración del motor de base de datos - Secuencia de archivo
  Utilice esta página para habilitar FILESTREAM para esta instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. FILESTREAM integra el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con una de archivos NTFS del sistema almacenando `varbinary(max)` datos de objeto binario grande (BLOB) como archivos en el sistema de archivos. [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden insertar, actualizar, consultar, buscar y realizar copias de seguridad de los datos FILESTREAM. Las interfaces del sistema de archivos de Win32 proporcionan el acceso de la transmisión por secuencias a los datos.  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Habilitar FILESTREAM para acceso Transact-SQL**  
 Seleccione esta opción para habilitar FILESTREAM para el acceso a [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este control debe comprobarse para que las otras opciones de control estén disponibles.  
  
 **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos**  
 Seleccione esta opción para habilitar el acceso de transmisión por secuencias de Win32 para FILESTREAM.  
  
 **Nombre de recurso compartido de Windows**  
 Utilice este control para escribir el nombre del recurso compartido de Windows en el que los datos de FILESTREAM se almacenarán.  
  
 **Permitir que los clientes remotos tengan acceso de transmisión por secuencias a los datos de FILESTREAM**  
 Seleccione este control para permitir que los clientes remotos tengan acceso a estos datos de FILESTREAM en este servidor.  
  
## <a name="see-also"></a>Vea también  
 [Habilitar y configurar FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
