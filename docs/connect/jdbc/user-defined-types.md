---
title: Tipos definidos por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 19a71b27-b788-43a3-a76d-fe3001a6f016
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ce45cb7fb76c1b01b57d96d86e34b051dc73043
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916951"
---
# <a name="user-defined-types"></a>Tipos definidos por el usuario

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Los tipos definidos por el usuario (UDT) se incorporaron en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para permitir a los desarrolladores extender el sistema de tipo escalar del servidor mediante el almacenamiento de objetos de Common Language Runtime (CLR) en una base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Los UDT pueden contener varios elementos y tener comportamientos, a diferencia de los tipos de datos de alias tradicionales, que se componen de un solo tipo de datos de sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anteriormente, los UDT estaban restringidos a un tamaño máximo de 8 kilobytes. En [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)], se ha agregado compatibilidad con UDT que superen los 64 kilobytes. A partir de la versión 3.0, el controlador JDBC también admite UDT de más de 64 kilobytes cuando se especifica el formato UserDefined.

No existe un cambio de comportamiento para los UDT con un tamaño menor o igual que 8.000 bytes, pero se admiten UDT de mayor tamaño y notifican su tamaño como "ilimitado".

## <a name="see-also"></a>Consulte también

[Descripción de los tipos de datos del controlador JDBC](../../connect/jdbc/understanding-the-jdbc-driver-data-types.md)
