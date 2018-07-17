---
title: Replicación de datos en columnas cifradas (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- encryption [SQL Server], replicating data
- encryption [SQL Server replication]
- publishing [SQL Server replication], encrypted columns
ms.assetid: d1f8f586-e5a3-4a71-9391-11198d42bfa3
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1995800b729a75861e43c846f3c2be7fdfd571cd
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350217"
---
# <a name="replicate-data-in-encrypted-columns-sql-server-management-studio"></a>Replicar datos en columnas cifradas (SQL Server Management Studio)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La replicación le permite publicar datos de columna cifrados. Para descifrar y usar estos datos en el suscriptor, la clave usada para cifrar los datos en el publicador también debe estar presente en el suscriptor. La replicación no ofrece un mecanismo de seguridad para transportar las claves de cifrado. Debe volver a crear manualmente la clave de cifrado en el suscriptor. En este tema se muestra cómo cifrar una columna en el publicador y asegurarse de que la clave de cifrado esté disponible en el suscriptor.  
  
 Los pasos básicos son los siguientes:  
  
1.  Cree la clave simétrica en el publicador.  
  
2.  Cifre los datos de la columna con la clave simétrica.  
  
3.  Publique la tabla con la columna cifrada.  
  
4.  Suscríbase a la publicación.  
  
5.  Inicialice la suscripción.  
  
6.  Vuelva a crear la clave simétrica en el suscriptor con los mismos valores para ALGORITHM, KEY_SOURCE e IDENTITY_VALUE que en el paso 1.  
  
7.  Obtenga acceso a los datos de columna cifrados.  
  
> [!NOTE]  
>  Debe usar una clave simétrica para cifrar los datos de columna. La propia clave simétrica puede protegerse mediante distintos métodos en el publicador y el suscriptor.  
  
### <a name="to-create-and-replicate-encrypted-column-data"></a>Para crear y replicar los datos de columna cifrados  
  
1.  En el publicador, ejecute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md).  
  
    > [!IMPORTANT]  
    >  El valor de KEY_SOURCE son datos importantes que pueden utilizarse para volver a crear la clave simétrica y descifrar los datos. KEY_SOURCE siempre debe almacenarse y transportarse de forma segura.  
  
2.  Ejecute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) para abrir la nueva clave.  
  
3.  Use la función [EncryptByKey](../../../t-sql/functions/encryptbykey-transact-sql.md) para cifrar los datos de columna en el publicador.  
  
4.  Ejecute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) para cerrar la clave.  
  
5.  Publique la tabla que contiene la columna cifrada. Para obtener más información, consulte [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md).  
  
6.  Suscríbase a la publicación. Para obtener más información, vea [Crear una suscripción de extracción](../../../relational-databases/replication/create-a-pull-subscription.md) o [Crear una suscripción de inserción](../../../relational-databases/replication/create-a-push-subscription.md).  
  
7.  Inicialice la suscripción. Para obtener más información, consulte [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md).  
  
8.  En el suscriptor, ejecute [CREATE SYMMETRIC KEY](../../../t-sql/statements/create-symmetric-key-transact-sql.md) con los mismos valores para ALGORITHM, KEY_SOURCE e IDENTITY_VALUE que en el paso 1. Puede especificar un valor distinto para ENCRYPTION BY.  
  
    > [!IMPORTANT]  
    >  El valor de KEY_SOURCE son datos importantes que pueden utilizarse para volver a crear la clave simétrica y descifrar los datos. KEY_SOURCE siempre debe almacenarse y transportarse de forma segura.  
  
9. Ejecute [OPEN SYMMETRIC KEY](../../../t-sql/statements/open-symmetric-key-transact-sql.md) para abrir la nueva clave.  
  
10. Use la función [DecryptByKey](../../../t-sql/functions/decryptbykey-transact-sql.md) para descifrar los datos replicados en el suscriptor.  
  
11. Ejecute [CLOSE SYMMETRIC KEY](../../../t-sql/statements/close-symmetric-key-transact-sql.md) para cerrar la clave.  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se crea una clave simétrica, un certificado que se usa para ayudar a proteger la clave simétrica y una clave maestra. Estas claves se crean en la base de datos de publicaciones y, a continuación, se usan para crear una columna cifrada (EncryptedCreditCardApprovalCode) en la tabla `SalesOrderHeader` . Esta columna se publica en la publicación AdvWorksSalesOrdersMerge en lugar de en la columna CreditCardApprovalCode no cifrada. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si debe almacenar las credenciales en un archivo de script, proteja el archivo para evitar el acceso no autorizado.  
  
 [!code-sql[HowTo#sp_PublishEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_1.sql)]  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_2.sql)]  
  
## <a name="example"></a>Ejemplo  
 En este ejemplo se vuelve a crear la misma clave simétrica en la base de datos de suscripciones con los mismos valores ALGORITHM, KEY_SOURCE e IDENTITY_VALUE del primer ejemplo. En este ejemplo se da por supuesto que ya ha inicializado una suscripción a la publicación AdvWorksSalesOrdersMerge para replicar la columna cifrada. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si tiene que almacenar credenciales en un archivo de script, debe proteger el archivo durante el almacenamiento y el transporte para evitar el acceso no autorizado.  
  
 [!code-sql[HowTo#sp_SubscriberEncryptedColumn](../../../relational-databases/replication/codesnippet/tsql/replicate-data-in-encryp_3.sql)]  
  
## <a name="see-also"></a>Ver también  
 [Información general sobre seguridad &#40;replicación&#41;](../../../relational-databases/replication/security/security-overview-replication.md)   
 [Crear claves simétricas idénticas en dos servidores](../../../relational-databases/security/encryption/create-identical-symmetric-keys-on-two-servers.md)  
  
  
