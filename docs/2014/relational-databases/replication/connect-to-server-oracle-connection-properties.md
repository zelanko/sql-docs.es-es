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
manager: craigg
ms.openlocfilehash: 479b0d562ffb78bc0003ca320eea0a85ab172430
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721699"
---
# <a name="connect-to-server-oracle-connection-properties"></a>Conectar al servidor (Oracle), Propiedades de conexión
  Use la **pestaña propiedades de conexión** del cuadro de diálogo **conectar con el servidor** para especificar una opción de publicación de puerta de **enlace** o **completo**. Después de identificar un publicador, esta opción no se puede cambiar sin quitar y volver a configurar el publicador. Para más información, vea [Configurar un publicador de Oracle](non-sql/configure-an-oracle-publisher.md).  
  
## <a name="options"></a>Opciones  
 **Tipo de publicador**  
 Seleccione **Puerta de enlace** o **Completo**. La opción **Completo** está diseñada para proporcionar publicaciones de instantáneas y transaccionales con todas las características compatibles con la publicación de Oracle. La opción **Puerta de enlace** proporciona optimizaciones de diseño específicas para mejorar el rendimiento en casos en los que la replicación sirva como puerta de enlace entre sistemas. La opción **Puerta de enlace** no se puede utilizar si tiene previsto publicar la misma tabla en varias publicaciones transaccionales. Una tabla puede aparecer como máximo en una publicación transaccional y en cualquier número de publicaciones de instantáneas si selecciona **Puerta de enlace**.  
  
 **Tiempos**  
 Especifique el tiempo que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el distribuidor debe intentar conectarse al publicador de Oracle antes de que se produzca un error de tiempo de espera.  
  
## <a name="see-also"></a>Consulte también  
 [Glosario de términos de publicaciones de Oracle](non-sql/glossary-of-terms-for-oracle-publishing.md)   
 [Optimizar el rendimiento de publicadores de Oracle](non-sql/performance-tuning-for-oracle-publishers.md)  
  
  
