---
title: Lenguaje de consulta estructurado (SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL [ODBC]
- SQL [ODBC], about SQL
- ODBC [ODBC], SQL
ms.assetid: bebfd93e-0dc0-46b3-a531-518beb7ea976
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c669b4424271fc1a3c91dea37159474fb52b97cd
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81293395"
---
# <a name="structured-query-language-sql"></a>Lenguaje de consulta estructurado (SQL)
Un DBMS típico permite a los usuarios almacenar, acceder y modificar datos de una manera organizada y eficaz. Originalmente, los usuarios de DBMS eran programadores. El acceso a los datos almacenados requiere la escritura de un programa en un lenguaje de programación como COBOL. Aunque estos programas solían escribirse para presentar una interfaz sencilla a un usuario no técnico, el acceso a los propios datos requería los servicios de un programador con conocimientos. El acceso esporádico a los datos no era práctico.  
  
 Los usuarios no estaban totalmente satisfechos con esta situación. Aunque podrían tener acceso a los datos, a menudo es necesario convencer a un programador DBMS para que escriba software especial. Por ejemplo, si un departamento de ventas deseara ver el total de ventas del mes anterior por cada uno de sus vendedores y quisiera que esta información se clasificara por orden en función de la duración del servicio de cada vendedor de la empresa, tenía dos opciones: ya existía un programa que permitía que se tuviera acceso a la información de la misma manera, o bien el Departamento tenía que pedir a un En muchos casos, esto era más trabajo del que mereceba, y siempre era una solución costosa para consultas puntuales o ad hoc. A medida que más usuarios quieran un acceso fácil, este problema aumentó más y más grande.  
  
 Permitir a los usuarios tener acceso a los datos de forma ad hoc, requiriendo un lenguaje en el que expresar sus solicitudes. Una única solicitud a una base de datos se define como una consulta; este tipo de lenguaje se denomina lenguaje de consulta. Se desarrollaron muchos lenguajes de consulta para este propósito, pero uno de ellos se convirtió en el más popular: Lenguaje de consulta estructurado, inventado en IBM en la década de 1970. Es más conocido por su acrónimo, SQL y se pronuncia como "ESS-CUE-ell" y como "seguido". SQL se convirtió en un estándar ANSI en 1986 y un estándar ISO en 1987; se usa hoy en muchos sistemas de administración de bases de datos.  
  
 Aunque SQL resolvió las necesidades ad hoc de los usuarios, la necesidad de acceso a los datos de los programas del equipo no desapareceba. De hecho, la mayor parte del acceso a la base de datos sigue siendo (y es) mediante programación, en forma de informes programados regularmente y análisis estadísticos, programas de entrada de datos como los que se usan para la entrada de pedidos y los programas de manipulación de datos, como los que se usan para conciliar cuentas y generar pedidos de trabajo.  
  
 Estos programas también usan SQL, mediante una de las tres técnicas siguientes:  
  
-   **SQL incrustado**, en el que las instrucciones SQL se incrustan en un lenguaje de host como C o COBOL.  
  
-   **Módulos de SQL**, en los que las instrucciones SQL se compilan en el DBMS y se llaman desde un lenguaje de host.  
  
-   **Interfaz de nivel de llamada**, o CLI, que consta de funciones llamadas para pasar instrucciones SQL al DBMS y recuperar los resultados del DBMS.  
  
> [!NOTE]  
>  Es un accidente histórico que se usa la interfaz de nivel de llamada en lugar de la interfaz de programación de aplicaciones (API), otro término para lo mismo. En el mundo de la base de datos, la API se usa para describir el propio SQL: SQL es la API de un DBMS.  
  
 De estas opciones, SQL incrustado es el que se usa con más frecuencia, aunque la mayoría de los DBMS principales admiten CLI de propiedad.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Procesar una instrucción SQL](../../odbc/reference/processing-a-sql-statement.md)  
  
-   [SQL incrustado](../../odbc/reference/embedded-sql.md)  
  
-   [Módulos SQL](../../odbc/reference/sql-modules.md)  
  
-   [Interfaces de nivel de llamada](../../odbc/reference/call-level-interfaces.md)
