---
title: 'Lección 1: crear Azure Storage cuenta y un contenedor | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: efdbd930-cde5-41b0-90ad-58a6cc68dddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4c0f364b15053e589d87b715d124bae48a87461e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85039867"
---
# <a name="lesson-1-create-azure-storage-account-and-container"></a>Lección 1: Crear la cuenta y el contenedor de Azure Storage
  Antes de empezar a almacenar SQL Server archivos de datos en Azure Storage, debe crear primero una cuenta de Azure Storage y un contenedor de blobs y una firma de acceso compartido. La lección 1 le guía por los pasos necesarios para iniciar sesión en Azure Portal de administración, crear una cuenta de almacenamiento, un contenedor de blobs y una firma de acceso compartido.  
  
 De forma predeterminada, solo el propietario de la cuenta de almacenamiento puede obtener acceso a los blobs, las tablas y las colas dentro de esa cuenta. Para tener acceso a estos recursos mediante esta nueva mejora de SQL Server sin compartir la clave de acceso de la cuenta de almacenamiento, es necesario hacer lo siguiente:  
  
-   Establecer como privados los permisos del contenedor.  
  
-   Crear una firma de acceso compartido. Esto le permite delegar el acceso restringido a un contenedor, un blob, una tabla o un recurso de cola especificando el intervalo para el que los recursos están disponibles y los permisos que un cliente tendrá en él.  
  
-   Utilice una directiva de acceso almacenada para administrar las firmas de acceso compartido de un contenedor o sus blobs. La directiva de acceso almacenado le ofrece una medida adicional de control sobre sus firmas de acceso compartido y también proporciona medios directos para revocarlas.  
  
 Para obtener más información, vea [administrar el acceso a recursos de Azure Storage](https://msdn.microsoft.com/library/windowsazure/ee393343.aspx).  
  
## <a name="create-storage-account"></a>Crear cuenta de almacenamiento  
 Para crear una cuenta de almacenamiento en Azure Portal de administración, siga estos pasos:  
  
1.  Inicie sesión en el [portal de administración de Azure](https://manage.windowsazure.com) con su cuenta. Si no tiene una cuenta de Azure, visite [Evaluación gratuita de Azure](https://www.windowsazure.com/pricing/free-trial/).  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-1.gif "SQL 14 CTP2")  
  
2.  Siga las instrucciones paso a paso para [crear una cuenta de almacenamiento](https://azure.microsoft.com/documentation/articles/storage-create-storage-account/). Tenga en cuenta que al crear una cuenta de almacenamiento que se usará para la característica archivos de datos de SQL Server en Azure, debe anular la selección o deshabilitar la replicación geográfica. Esto se debe a que el orden de escritura no se garantiza para los distintos blobs que participen en la replicación geográfica. Si se georreplica una cuenta de almacenamiento y se requiere la recuperación, se producen daños.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-2.gif "SQL 14 CTP2")  
  
## <a name="create-a-blob-container"></a>Crear un contenedor de blobs  
 En Azure, un contenedor proporciona una agrupación de un conjunto de blobs. Todos los blobs deben estar en un contenedor. Una cuenta de almacenamiento puede contener un número ilimitado de contenedores, pero debe tener al menos uno. Un contenedor puede almacenar un número ilimitado de blobs. Para obtener la información más actualizada sobre los límites de tamaño de almacenamiento, vea [Cómo usar el servicio de Azure BLOB Storage en .net](https://www.windowsazure.com/develop/net/how-to-guides/blob-storage/).  
  
 Para crear un contenedor en Azure, siga estos pasos:  
  
1.  Inicie sesión en el [Portal de administración de Azure](https://manage.windowsazure.com).  
  
2.  Seleccione la cuenta de almacenamiento, haga clic en la pestaña **contenedores** y haga clic en **Agregar contenedor** en la parte inferior de la pantalla, que abre un nuevo cuadro de diálogo.  
  
3.  Escriba un nombre para el contenedor.  
  
4.  Seleccione **privado** para **tipo de acceso**. Al establecer el acceso en privado, solo el propietario de la cuenta de Azure puede leer los datos del contenedor y del BLOB.  
  
     ![SQL 14 CTP2](../../2014/tutorials/media/ss-was-tutlesson-1-4.gif "SQL 14 CTP2")  
  
> [!NOTE]  
>  Para crear un contenedor mediante programación, también puede usar las API de REST. Para obtener más información, vea [crear contenedor](https://msdn.microsoft.com/library/windowsazure/dd179468.aspx) y también [Azure Storage referencia](https://msdn.microsoft.com/library/windowsazure/dd179355.aspx)de la API de REST de servicios.  
  
 **Lección siguiente:**  
  
 [Lección 2. Crear una directiva en el contenedor y generar una firma de acceso compartido &#40;clave de&#41; SAS](../relational-databases/lesson-1-create-stored-access-policy-and-shared-access-signature.md)  
  
