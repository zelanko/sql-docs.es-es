---
title: Conexión al servidor (Oracle) y propiedades de conexión | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.oracleconnection.connectionprops.f1
helpviewer_keywords:
- Connect to Server dialog box, replication
ms.assetid: 1bb7396f-cbb2-4f88-b82b-543287ed4172
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4c76a3058283a098357701a44de48efff917acd7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010950"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Conectar al servidor (Oracle), Propiedades de conexión
  Utilice la pestaña **Propiedades de conexión** del cuadro de diálogo **Conectar al servidor** para especificar una opción de publicación de **Puerta de enlace** o **Completo**. Después de identificar un publicador, esta opción no se puede cambiar sin quitar y volver a configurar el publicador. Para obtener más información, vea [Configurar un publicador de Oracle](non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opciones  
 **Tipo de anunciante**  
 Seleccione **Puerta de enlace** o **Completo**. La opción **Completo** está diseñada para proporcionar publicaciones de instantáneas y transaccionales con todas las características compatibles con la publicación de Oracle. La opción **Puerta de enlace** proporciona optimizaciones de diseño específicas para mejorar el rendimiento en casos en los que la replicación sirva como puerta de enlace entre sistemas. La opción **Puerta de enlace** no se puede utilizar si tiene previsto publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantáneas si selecciona **Puerta de enlace**.  
  
 **Tiempos de espera**  
 Especifique el tiempo durante el que el distribuidor de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe intentar conectarse con el publicador de Oracle antes de que se produzca un error de tiempo de expiración.  
  
## <a name="see-also"></a>Consulte también  
 [Glosario de términos de publicaciones de Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Optimizar el rendimiento de publicadores de Oracle](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
