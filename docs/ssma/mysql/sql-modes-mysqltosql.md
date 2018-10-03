---
title: Modos de SQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d840ee51-b863-4e77-84aa-37d3f094bfed
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 46d91efa1451749d8d1cce2b1a8cf361cc30986a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47737313"
---
# <a name="sql-modes-mysqltosql"></a>Modos DE SQL (MySQLToSQL)
SSMA para MySQL puede funcionar en diferentes modos de SQL y puede aplicar estos modos de forma diferente para distintos clientes.  
  
Modos de definen la sintaxis SQL que debe ser compatibles con MySQL y el tipo de validación de datos comprueba que debe realizar. Esto hace más fácil de usar MySQL en entornos diferentes y usar MySQL con SQL Server.  
  
## <a name="sql-modes-grid"></a>Cuadrícula de los modos SQL:  
  
-   Cuadrícula de modos de SQL en el nivel de raíz contiene las siguientes columnas: **SQL nombre de modo**, **cargado modos SQL**, y **eficaz de los modos de SQL**.  
  
-   Cuadrícula de los modos de SQL en bases de datos categoría, base de datos, tabla categoría, categoría de instrucciones, categoría de vistas, tabla, vista, funciones, procedimientos, UDF y nivel de objeto de evento contiene las siguientes columnas: **SQL nombre de modo**,  **Heredan los modos SQL**, y **modos eficaces SQL**.  
  
-   Cuadrícula de modos de SQL en el nivel de procedimiento almacenado, función almacenado y desencadenador contiene las siguientes columnas: **SQL nombre de modo**, **Original de los modos de SQL**, y **eficaz de los modos de SQL**.  
  
> [!NOTE]  
> Modos de grupo se mostrará en negrita, en la columna 'Nombre de modo SQL'.  
  
## <a name="loaded-sql-modes"></a>Modos de SQL cargado  
Estos son los modos de SQL, que se establecen en el nivel raíz o de sesión. Los modos de SQL una vez cargadas en la base de datos de destino no puede editarse o modificarse.  
  
## <a name="inherited-sql-modes"></a>Modos de SQL heredadas  
Estos son los modos de SQL, que se heredan desde el nodo primario correspondiente.  
  
Excepto la categoría de funciones, procedimientos (categoría), categoría de eventos y desencadenadores, estos modos de SQL están presentes en todos los niveles (objeto de base de datos, tabla categoría, categoría de instrucciones, las vistas categoría, tabla, vista, funciones, procedimientos, UDF y eventos).  
  
> [!NOTE]  
> Si selecciona el **heredar de primario** casilla de verificación, heredan los modos de SQL se pueden heredar el nodo primario. De forma predeterminada, esta casilla permanece seleccionada.  
  
## <a name="original-sql-modes"></a>Modos originales de SQL  
Estos son los modos de SQL está presente sólo en función, procedimiento y desencadenador niveles.  
  
> [!NOTE]  
> Seleccionando la **utilizar original** comprobar cuadro, los modos de SQL que se usaron originalmente en la función correspondiente o se puede usar el procedimiento o desencadenador. De forma predeterminada, esta casilla permanece seleccionada.  
  
## <a name="effective-sql-modes"></a>Modos de efectivo SQL  
Modos eficaz de SQL se pueden definir en distintos niveles en la siguiente manera:  
  
-   **En el nivel de sesión:**  
  
    1.  Todos los modos de SQL de carga se puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, los modos SQL efectivos pueden directamente y explícitamente modificarse.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo de carga de SQL y, por último, se aplica al objeto.  
  
-   **En el nivel de función o procedimiento o desencadenador:**  
  
    1.  Todos los modos de SQL Original se puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, el modo eficaz de SQL puede explícitamente modificarse únicamente cuando el **utilizar original** casilla esté desactivada.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo Original de SQL y, por último, se aplica al objeto.  
  
-   **En los nodos que no son de nivel de función o procedimiento o desencadenador:**  
  
    1.  Todos los modos de SQL heredada se puede llamar, "Modos eficaz de SQL".  
  
    2.  En este nivel, el modo eficaz de SQL puede explícitamente modificarse únicamente cuando el **heredar de primario** casilla esté desactivada.  
  
    3.  El modo eficaz de SQL que se establece explícitamente no se refleja como modo heredado de SQL y, por último, se aplica al objeto.  
  
