---
title: Información de parámetros (IntelliSense) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Parameter Info option [IntelliSense]
- stored function parameter completion [Intellisense]
- language references [SQL Server]
- IntelliSense [SQL Server], Parameter Info option
ms.assetid: 56c2aac9-c65c-4679-b62c-d9f689876dde
author: markingmyname
ms.author: maghan
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 015e0708b9e43340918bbf4d6d207c2b12a34c64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65821295"
---
# <a name="parameter-info-intellisense"></a>Información de parámetros (IntelliSense)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  La opción [!INCLUDE[msCoName](../../includes/msconame-md.md)] Información de parámetros **de** IntelliSense abre una lista de parámetros que proporciona información sobre el número, los nombres y los tipos de parámetros necesarios para una función o un procedimiento almacenado. El parámetro en negrita indica el siguiente parámetro que se necesita al escribir una función o un procedimiento almacenado.  
  
 La lista de parámetros también aparece para las funciones anidadas. Si se escribe una función como parámetro de otra función, la lista de parámetros muestra los parámetros de la función interna. Así, cuando la lista de parámetros de la función interna está completa, pasa a mostrar los parámetros de la función externa.  
  
#### <a name="to-view-parameter-info-for-functions-or-stored-procedures"></a>Para ver la información de parámetros de funciones o procedimientos almacenados del sistema  
  
1.  Tras el nombre de una función, escriba un paréntesis de apertura como haría para abrir la lista de parámetros. Después de escribir el nombre de un procedimiento almacenado, escriba un espacio como haría para obtener información sobre los parámetros del procedimiento.  
  
     IntelliSense muestra la declaración completa de la función o los parámetros del procedimiento almacenado en una ventana emergente situada bajo el punto de inserción. El primer parámetro de la lista aparece en negrita.  
  
2.  A medida que escribe los parámetros, el formato en negrita cambia para reflejar el siguiente parámetro que hay que especificar.  
  
3.  Presione ESC en cualquier momento para cerrar la lista o siga escribiendo hasta que haya completado la función.  
  
     En una función, al escribir el paréntesis de cierre se cierra también la lista de parámetros.  
  
#### <a name="to-manually-start-parameter-info"></a>Para iniciar manualmente Información de parámetros  
  
1.  En el menú **Edición** , seleccione **IntelliSense** y, a continuación, seleccione **Información de parámetros**.  
  
2.  Presione las teclas del método abreviado CTRL+MAYÚS+ESPACIO.  
  
 Para obtener más información, vea [Configurar IntelliSense &#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md).  
  
> [!NOTE]  
>  La opción **Información de parámetros** solo está disponible para el Editor de consultas de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y el Editor de consultas XML.  
  
  
