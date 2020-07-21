---
title: Propiedades de Alias (pestaña Alias)
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: 2d1498e2-129c-4ce7-88e5-408e4037243c
author: markingmyname
ms.author: maghan
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 53bb19934209ee501c76317e102e5b1fcae28c4d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75306605"
---
# <a name="ltaliasgt-properties-alias-tab"></a>Propiedades de &lt;Alias&gt; (pestaña Alias)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Un alias es un nombre alternativo que se puede utilizar para establecer una conexión. El alias encapsula los elementos necesarios de una cadena de conexión y los expone con un nombre elegido por el usuario. Use la página **Alias** del cuadro de diálogo **\<** Nombre de alias **> Propiedades** para ver o especificar los elementos de la cadena de conexión de un alias.

## <a name="options"></a>Opciones

**Nombre de alias**

Nombre (alias) que desee usar para hacer referencia a esta conexión.  

**Nombre de canalización** / **Número de puerto**  

Elementos adicionales de la cadena de conexión. El nombre de este cuadro varía según el protocolo seleccionado. Vea los temas enumerados a continuación para obtener ejemplos.  

**Protocolo**

Protocolo utilizado para la conexión.

**Server**

Nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que se va a conectar.  

## <a name="see-also"></a>Consulte también

- [Crear una cadena de conexión válida con el protocolo de memoria compartida](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)
- [Crear una cadena de conexión válida con TCP/IP](../../tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)
- [Crear una cadena de conexión válida con canalizaciones con nombre](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)