---
title: Agregar y comprobar una conexión de datos o un origen de datos (Generador de informes y SSRS) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 03/01/2017
ms.openlocfilehash: 9b8eca48287388eba7f8e1f13ba4c6e5692a278d
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68251064"
---
# <a name="add-and-verify-a-data-connection-report-builder-and-ssrs"></a>Agregar y comprobar una conexión de datos o un origen de datos (Generador de informes y SSRS)

En el Generador de informes, puede agregar un origen de datos compartido del servidor de informes o crear un origen de datos incrustado para el informe. En el Diseñador de informes, puede crear un origen de datos compartido o un origen de datos incrustado e implementarlo en un servidor de informes.

Para agregar un origen de datos compartido al informe, busque un servidor de informes y seleccione un origen de datos compartido. El origen de datos compartido del informe señala a la definición del origen de datos compartido en el servidor de informes.

Para crear un origen de datos incrustado, debe disponer de la información de la conexión al origen de datos externo y saber qué permisos necesita para el acceso a los datos. Esta información normalmente procede del propietario del origen de datos. Puede probar la conexión para comprobar que las credenciales que se especifican son suficientes.

Para obtener más información, vea [Conexiones de datos, orígenes de datos y cadenas de conexión (Generador de informes y SSRS)](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) y [Especificar credenciales en el Generador de informes](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017).

> [!NOTE]  
> [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]

## <a name="to-create-a-connection-to-a-shared-data-source-in-report-builder"></a>Para crear una conexión a un origen de datos compartido en el Generador de informes

1. En la barra de herramientas del panel Datos de informe, haga clic en **Nuevo** y, a continuación, haga clic en **Origen de datos**. Se abre el cuadro de diálogo **Propiedades del origen de datos** .

2. En el cuadro de texto **Nombre** , escriba un nombre para el origen de datos.

    > [!NOTE]  
    >  Este nombre se guarda en la definición de informe local. No es el nombre del origen de datos compartido del servidor de informes. 

3. Seleccione **Usar una conexión compartida en el modelo de informe**. Aparece la lista de modelos de informe y orígenes de datos compartidos usados recientemente. Para seleccionar uno de un servidor de informes, haga clic en **Examinar** y busque la carpeta del servidor de informes en la que están disponibles los orígenes de datos compartidos.

4. Seleccione el origen de datos compartido y, a continuación, haga clic en **Abrir**.

5. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

El origen de datos aparece en el panel Datos de informe.

### <a name="to-verify-a-data-connection"></a>Para comprobar una conexión de datos  

1. En la barra de herramientas del panel Datos de informe, haga doble clic en el origen de datos. Se abre el cuadro de diálogo **Propiedades del origen de datos** .

2. Haga clic en **Probar conexión**.

3. Si la conexión es correcta, aparece el mensaje siguiente: "Conexión creada correctamente". [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

4. Si la conexión no es correcta, aparece un mensaje similar al siguiente: "No se puede establecer conexión con el origen de datos".  

5. Haga clic en **Detalles**y utilice la información para corregir el problema.

    Para más información, vea [Especificar credenciales en el Generador de informes](https://docs.microsoft.com/sql/reporting-services/report-data/specify-credential-and-connection-information-for-report-data-sources?view=sql-server-2017).

6. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  

## <a name="see-also"></a>Vea también

- [Conjuntos de datos de informe &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
- [Conjuntos de datos incrustados y compartidos de informe &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)
- [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](../../reporting-services/report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)
- [Conexiones de datos, orígenes de datos y cadenas de conexión en el Generador de informes](data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)