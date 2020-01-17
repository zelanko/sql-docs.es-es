---
title: 'MSSQLSERVER: error del Motor de base de datos | Microsoft Docs'
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 823 (Database Engine error)
ms.assetid: 0d9fce3c-3772-46ce-a7a3-4f4988dc6cae
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8a678fe4fdda95710b6e6707f922a9d0c1c9d732
ms.sourcegitcommit: a02727aab143541794e9cfe923770d019f323116
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2020
ms.locfileid: "75755869"
---
# <a name="mssqlserver---database-engine-error"></a>MSSQLSERVER: error del Motor de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|823|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|B_HARDERR|  
|Texto del mensaje|El sistema operativo ha devuelto el error %ls en SQL Server durante %S_MSG en el desplazamiento %#016I64x del archivo '%ls'. Encontrará más detalles en los mensajes adicionales del registro de errores de SQL Server y el registro de eventos del sistema. Se trata de una condición de error grave de nivel de sistema que amenaza a la integridad de la base de datos y que debe corregirse inmediatamente. Ejecute una comprobación de coherencia completa de la base de datos (DBCC CHECKDB). Este error puede deberse a muchos factores. Para obtener más información vea los Libros en pantalla de SQL Server.|  
  
## <a name="explanation"></a>Explicación  
Error de solicitud de lectura o escritura de Windows. El código de error devuelto por Windows y el texto correspondiente se insertan en el mensaje. En el caso de la solicitud de lectura, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya la habrá intentado cuatro veces. Suele ser el resultado de un error de hardware, pero puede estar causado por el controlador del dispositivo. Para obtener más información sobre el error 823, consulte [El mensaje de error 823 puede indicar problemas de hardware o del sistema en SQL Server](https://support.microsoft.com/kb/828339). Para obtener más información sobre los errores de E/S, vea el [capítulo 2 del documento sobre conceptos básicos de E/S de Microsoft SQL Server](/previous-versions/sql/sql-server-2005/administrator/cc917726(v=technet.10)).  
  
## <a name="user-action"></a>Acción del usuario  
Busque información adicional en el registro de eventos del sistema. Póngase en contacto con el fabricante del hardware o el servicio de Soporte técnico y Atención al cliente de Microsoft para determinar la causa y la acción correctora. Después de solucionar el error de hardware, restaure todas las bases de datos y ejecute DBCC CHECKDB.  
  
