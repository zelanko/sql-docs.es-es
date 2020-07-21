---
title: 'Lección 2: Especificación de información de conexión (Reporting Services) | Microsoft Docs'
description: En esta lección, va a definir un origen de datos, la información de conexión que el informe usa para acceder a los datos desde una base de datos relacional u otros orígenes.
ms.date: 12/09/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9d4e12a0322a35e96bd930c4fa6f1f852daf2bdd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75258463"
---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lección 2: Especificación de información de conexión (Reporting Services)

En la lección 1, agregó un informe paginado de [!INCLUDE[ssrsnoversion-md](../includes/ssrsnoversion-md.md)] al proyecto Tutorial.
  
En esta lección, va a definir un *origen de datos*, la información de conexión que el informe usa para acceder a los datos desde una base de datos relacional u otros orígenes.

Para este informe, va a agregar la base de datos de ejemplo AdventureWorks2016 como el origen de datos. En este tutorial se da por hecho que esta base de datos se encuentra en la instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] instalada en el equipo local.  

## <a name="to-set-up-a-connection"></a>Para configurar una conexión  

1. En el panel **Datos de informe**, seleccione **Nuevo** > **Origen de datos**. Si el panel **Datos de informe** no aparece, seleccione el menú **Ver** > **Datos de informe**.

    ![ssrs-table-tutorial-2-new-data-source](media/ssrs-table-tutorial-2-new-data-source.png)

    El cuadro de diálogo **Propiedades de origen de datos** se abre y en él se muestra la sección **General**.

    ![Cuadro de diálogo Propiedades de origen de datos](media/lesson-2-specifying-connection-information-reporting-services/vs-datasource-connection-properties-dialog-box.png)

2. En el cuadro de texto **Nombre**, escriba "AdventureWorks2016".

3. Seleccione el botón de radio **Conexión insertada**.

4. En el cuadro de selección desplegable **Tipo**, seleccione "Microsoft SQL Server".
  
5. En el cuadro de texto **Cadena de conexión**, escriba la siguiente cadena:

    `Data source=localhost; initial catalog=AdventureWorks2016`

    > [!NOTE]
    > Esta cadena de conexión da por supuesto que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el servidor de informes y la base de datos AdventureWorks2016 están instalados en el equipo local.
    >
    >Cambie la cadena de conexión y reemplace “localhost” por el nombre del servidor o la instancia de base de datos, en caso de que la hipótesis sea cierta. Si usa [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] o una instancia con nombre de SQL Server, deberá modificar la cadena de conexión para incluir la información de la instancia. Por ejemplo:
    >
    > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2016`
    >
    > Para más información sobre las cadenas de conexión, puede consultar la sección `See also` a continuación.

6. Seleccione la pestaña **Credenciales** y, en la sección **Cambiar las credenciales utilizadas para conectarse al origen de datos**, seleccione el botón de radio **Usar autenticación de Windows (seguridad integrada)** .

7. Seleccione **Aceptar** para completar el proceso.

El Diseñador de informes agrega el origen de datos AdventureWorks2016 al panel **Datos de informe**.

![ssrs-adventureworks-datasource](media/lesson-2-specifying-connection-information-reporting-services/ssrs-adventureworks-datasource2016.png)

## <a name="next-steps"></a>Pasos siguientes

En esta lección, ha definido correctamente una conexión a la base de datos de ejemplo AdventureWorks2016. Continúe con [Lección 3: Definir un conjunto de datos para el informe de tabla &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md) para definir un conjunto de datos para el informe.

## <a name="see-also"></a>Consulte también

[Creación de cadenas de conexión de datos - Generador de informes y SSRS](report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)
