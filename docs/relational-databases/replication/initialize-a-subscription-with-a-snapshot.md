---
title: Inicializar una suscripción con una instantánea | Microsoft Docs
ms.custom: ''
ms.date: 03/23/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], initializing subscriptions
- initializing subscriptions [SQL Server replication], snapshots
ms.assetid: 77a9ade2-cdc0-4ae9-a02d-6e29d7c2ada0
author: MashaMSFT
ms.author: mathoma
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 44ccd31700ab6bb3bf3500e93febc0209d9fa9ee
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716782"
---
# <a name="initialize-a-subscription-with-a-snapshot"></a>Inicializar una suscripción con una instantánea

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

En este artículo se describen los procesos que se producen cuando se inicializa una publicación de replicación. Se aplica una instantánea inicial a los suscriptores.

## <a name="snapshot-for-a-new-publication"></a>Instantánea para una publicación nueva

De forma predeterminada, se captura una instantánea después de crear una publicación.
La instantánea se copia en la carpeta de instantáneas. Este comportamiento predeterminado se produce para las publicaciones de mezcla creadas con el Asistente para nueva publicación.

### <a name="snapshot-is-applied-to-subscriber"></a>La instantánea se aplica al suscriptor

Un agente aplica la instantánea nueva al suscriptor. La aplicación se realiza durante la sincronización inicial de la suscripción. El agente que realiza la aplicación depende del tipo de publicación:

- Para las publicaciones _transaccionales_ y de _instantáneas_:
  - Agente de distribución.

- Para las publicaciones de _mezcla_:
  - Agente de mezcla.

### <a name="type-of-publication"></a>Tipo de publicación

En la tabla siguiente se muestra el contenido de la instantánea, para cada tipo de publicación.

&nbsp;

| Tipo de publicación de la instantánea | Contenido de la instantánea |
| :---------------------------------------- | :----------------------- |
| <ul> <li>Publicación de instantáneas</li> <li>Publicación transaccional</li> <li>Publicación de mezcla que no usa filtros con parámetros</li> </ul> | <ul> <li>Schema</li> <li>Datos, en archivos para el programa de copia masiva (BCP)</li> <li>Restricciones</li> <li>Propiedades extendidas</li> <li>Índices</li> <li>Desencadenadores</li> <li>Tablas del sistema necesarias para la replicación</li> </ul> <br/>Vea [Creación y aplicación de la instantánea](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md). |
| <ul> <li>Publicación de mezcla que usa filtros con parámetros</li> </ul> | <ul> <li>Instantánea de esquema (scripts de replicación, objetos publicados, pero sin datos)</li> <li>Datos que pertenecen a la partición de la suscripción</li> </ul> <br/>Vea [Instantáneas para publicaciones de mezcla con filtros con parámetros](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md). |
| | |

#### <a name="two-part-process-with-merge-publication-that-uses-parameterized-filters"></a>Proceso de dos partes con publicación de mezcla que usa filtros con parámetros

Para una publicación de mezcla que usa filtros con parámetros, la instantánea se crea mediante el siguiente proceso de dos partes:

1. Se crea una instantánea de esquema, que contiene los elementos siguientes:
   - Scripts de replicación.
   - Esquema de los objetos publicados.
   - _(Pero sin datos)._

2. Después, cada suscripción se inicializa con una instantánea. La instantánea incluye los elementos siguientes:
   - Scripts y esquema, copiados de la instantánea de esquema.
   - Datos que pertenecen a la partición de la suscripción.

## <a name="type-of-replication"></a>Tipo de replicación

Los tipos de archivo incluidos en la instantánea dependen del tipo de replicación y de los artículos de la publicación.

&nbsp;

| Tipo de replicación | Archivos comunes de instantánea |
| :------------------ | :-------------------- |
| Replicación de instantáneas, o bien<br/>Replicación transaccional | &bullet; Esquema (.sch) <br/>&bullet; Datos (.bcp) <br/>&bullet; Restricciones e índices (.dri) <br/>&bullet; Archivos de instantánea comprimidos (.cab) <br/>&bullet; Desencadenadores (.tag), solo para actualizar un suscriptor <br/><br/>&bullet; Restricciones (.idx) |
| Replicación de mezcla                                      | &bullet; Esquema (.sch) <br/>&bullet; Datos (.bcp) <br/>&bullet; Restricciones e índices (.dri) <br/>&bullet; Archivos de instantánea comprimidos (.cab) <br/>&bullet; Desencadenadores (.trg) <br/><br/>&bullet; Datos de tabla del sistema (.sys) <br/>&bullet; Tablas de conflictos (.cft) |
| | |

### <a name="snapshot-folder"></a>Carpeta de instantáneas

Para transferir los archivos, se copian en la _carpeta de instantáneas_ predeterminada, o bien en la _carpeta alternativa_ para las instantáneas.

La carpeta de instantáneas se especifica cuando se configura el distribuidor. La carpeta alternativa se especifica cuando se crea la publicación.

### <a name="resume-transfer-after-interruption"></a>Reanudación de la transferencia después de la interrupción

La transferencia de archivos a una carpeta de instantáneas se reanuda de forma automática si una conexión no confiable interrumpe la transferencia.

Por motivos de eficacia, la reanudación no reenvía ningún archivo que ya se haya transferido de forma completa antes de la interrupción.

## <a name="snapshot-options"></a>Opciones de instantánea

Hay una serie de opciones disponibles al inicializar una suscripción con una instantánea. Puede:

- Especificar una ubicación alternativa para la carpeta de instantáneas en lugar de, o además de, la predeterminada. Para más información, vea [Modificación de las opciones de la instantánea](../../relational-databases/replication/snapshot-options.md).

- Comprimir instantáneas para su almacenamiento en medios extraíbles o para su transferencia a través de una red lenta. Para más información, consulte [Compressed Snapshots](../../relational-databases/replication/snapshot-options.md#compressed-snapshots).

- Ejecutar scripts Transact-SQL antes o después de aplicar la instantánea. Para obtener más información, consulte [Ejecutar scripts antes y después de aplicar la instantánea](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied).

- Transferir la instantánea mediante el Protocolo de transferencia de archivos (FTP). Para obtener más información, vea [Transferir instantáneas mediante FTP](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md).

## <a name="see-also"></a>Consulte también

[Inicializar una suscripción](../../relational-databases/replication/initialize-a-subscription.md)

[Proteger la carpeta de instantáneas](../../relational-databases/replication/security/secure-the-snapshot-folder.md)
