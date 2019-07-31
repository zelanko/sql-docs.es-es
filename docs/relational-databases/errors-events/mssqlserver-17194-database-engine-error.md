---
title: MSSQLSERVER_17194 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
f1_keywords:
- "17194"
helpviewer_keywords:
- 17194 (Database Engine error)
ms.assetid: 0d03eb20-28a7-4ceb-8903-7f9420a620f7
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 47678d81d2868af5a921d26f3e121837a1ddc938
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131729"
---
# <a name="mssqlserver17194"></a>MSSQLSERVER_17194
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17194|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico||  
|Texto del mensaje|El servidor no pudo cargar la biblioteca de proveedores SSL necesaria para el inicio de sesión; se cerró la conexión. SSL se utiliza para cifrar la secuencia de inicio de sesión o todas las comunicaciones, según el modo en que el administrador haya configurado el servidor. Consulte los Libros en pantalla para obtener información sobre este mensaje de error:  0xXXXX. [CLIENTE: 11.11.11.11]|  
  
## <a name="explanation"></a>Explicación  
Este error indica que el cliente ha cerrado la conexión. Este error se produce porque se ha agotado el tiempo de espera de la conexión. El mensaje de error muestra un valor del sistema operativo que describe el problema subyacente.  
  
## <a name="user-action"></a>Acción del usuario  
Si el código de error incluido en el mensaje es 0x2746 (valor decimal 10054), significa que el cliente ha restablecido la conexión debido, normalmente, a que se ha agotado el tiempo de espera. Para solucionar el error, aumente el tiempo de espera de la conexión en el cliente o en el programa que realiza la llamada.  
  
Para determinar una posible solución para otros valores de mensaje de error, use el comando de sistema operativo **net helpmsg** y especifique el valor decimal del código de error.  
  
Para obtener más información sobre cómo conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Server Network Configuration](~/database-engine/configure-windows/server-network-configuration.md) (Configuración de red del servidor) y [Client Network Configuration](~/database-engine/configure-windows/client-network-configuration.md) (Configuración de red del cliente).  
  
## <a name="internal-only"></a>Solo para uso interno  
