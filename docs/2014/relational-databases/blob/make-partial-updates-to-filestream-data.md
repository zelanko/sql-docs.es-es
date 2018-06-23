---
title: Realización de actualizaciones parciales de los datos FILESTREAM | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FILESTREAM [SQL Server], FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
- FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT
ms.assetid: d6f7661e-6c14-4d31-9541-4520ca0f82b2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c59d3e7823efe62ecb7227eab605af23a6ea3112
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103329"
---
# <a name="make-partial-updates-to-filestream-data"></a>Realizar actualizaciones parciales de los datos FILESTREAM
  Una aplicación utiliza FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT para realizar actualizaciones parciales de los datos de FILESTREAM BLOB. La función [DeviceIoControl](http://go.microsoft.com/fwlink/?LinkId=105527) pasa este valor y el controlador que [OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md) devuelve al controlador FILESTREAM. A continuación, el controlador obliga a hacer una copia del lado servidor de los datos FILESTREAM actuales en el archivo al que el controlador hace referencia. Si la aplicación emite el valor FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT una vez escrito el controlador, la última operación de escritura se conserva y se pierden las operaciones de escritura anteriores que se realizaron en el controlador.  
  
> [!NOTE]  
>  FILESTREAM se basa en el protocolo [SMB protocol](http://go.microsoft.com/fwlink/?LinkId=112454) para el acceso remoto.  
  
## <a name="example"></a>Ejemplo  
 En el ejemplo siguiente se muestra cómo utilizar el valor `FSCTL_SQL_FILESTREAM_FETCH_OLD_CONTENT` para realizar una actualización parcial de un FILESTREAM BLOB insertado.  
  
> [!NOTE]  
>  Este ejemplo requiere la tabla y la base de datos habilitadas para FILESTREAM que se crean en [Crear una base de datos habilitada para FILESTREAM](create-a-filestream-enabled-database.md) y [Crear una tabla para almacenar datos FILESTREAM](create-a-table-for-storing-filestream-data.md).  
  
 [!code-cpp[FILESTREAM#FS_CPP_FSCTL](../../snippets/tsql/SQL15/tsql/filestream/cpp/filestream.cpp#fs_cpp_fsctl)]  
  
## <a name="see-also"></a>Vea también  
 [Obtener acceso a los datos FILESTREAM con OpenSqlFilestream](access-filestream-data-with-opensqlfilestream.md)   
 [Crear aplicaciones cliente para datos FILESTREAM](create-client-applications-for-filestream-data.md)  
  
  