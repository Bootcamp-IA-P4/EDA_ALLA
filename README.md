# PROYECTO EDA-MINIDATHATON

En este IV proyecto de **Factoría F5** se me pidió realizar un EDA (Análisis Exploratorio de Datos) completo sobre cualquier base de datos en formato csv, haciendo una exploración de esos datos y elaborando un informe con las conclusiones y los descubrimientos. 

Para esto he usado mi proyecto anterior de **Web-Scraping de Infojobs**, para crear *mi propia base de datos* sobre ofertas de trabajo de tecnología en España. Por eso, he decidio seleccionar los sectores tecnológicos más comunes y hacer el análisis sobre estos datos

**Los términos de búsqueda han sido:**

- Full Stack
- Frontend
- Backend
- Data Scients
- Data Engineer
- Inteligencia Artificial
- Azure Cloud
- AWS cloud
- Especialista en Ciberseguridad
- Machine Learning
- Hardware Engineer

Con estos términos de búsqueda he recopilado **2586 ofertas** de trabajo y los he guardado en un archivo llamado [job_offers_rows.csv](https://github.com/alharuty/Proyecto-EDA-MiniDathaton/blob/main/job_offers_rows.csv) para su posterior estudio.

Para el correcto análisis he tenido que hacer limpieza en varias columnas de la tabla:<br>
  1. **Columna salary:** Debido a que en la tabla original los salarios están representados en tipo string, he decidido crear una función para la limpieza de esa columna y que así sea más fácil manejar los salarios:<br>
    - **Convertir los string en int:**<br>
    - **Hacer una media del rango del salario para cada oferta de trabajo:** pasar de "30.000 € - 36.000 € Bruto/año" a 33.000<br>
    - **Cambiar el "No disponible" por NaN**<br>
    - **Si encuentra un salario que dice "Más de X€"**, dejarlo simplemente en X<br>
  2. **Limpieza de duplicados:** Viendo las estadísticas básicas, me he dado cuenta que de las 2586 ofertas(title) sólo 1566 son únicos. Esto es un fallo del scraper, porque no elimina las ofertas duplicadas. Pero tras estudiar la tabla, he tenido en cuenta que puede que haya un mísmo título pero que sea diferente oferta de trabajo, diferente empresa, diferente jornada laboral, etc.<br>
  
**Por ejemplo:** <br>

Data engineer | Empresa 1 | Madrid | 30000€<br>
Data engineer | Empresa 2 | Barcelona | 32000€<br>

Vemos que hay un mísmo título pero son 2 ofertas diferentes, teniendo en cuenta esto, la cifra de duplicados baja porque puede que por algún casual haya 2 ofertas con el mismo nombre, porque estos no son unique. 

Entonces, he decidido buscar los **duplicados** que tengan **todas** las columnas iguales:

**Por ejemplo:** <br>
    
Data engineer | Empresa 1 | Madrid | 30000€<br>
Data engineer | Empresa 1 | Madrid | 30000€<br>

En este caso vamos a limpiar la tabla, dejando solo la primera coincidencia.<br>

Ahora que tenemos los datos limpios, he decidido crear una nueva tabla (new_db) sólo con las columnas que voy a necesitar y además renombrarlos traduciendo de inglés a español para una mejor comprensión:

- search_term => Puesto de trabajo
- location => Ciudad
- salary_clean => Salario
- work_mode => Forma de trabajo
- contract_type => Tipo de contrato
- workday => Tipo de jornada
- company => Empresa

La tabla limpia se ve así: 👇
<img width="1164" alt="Captura de pantalla 2025-04-01 a las 9 15 33" src="https://github.com/user-attachments/assets/60365d5c-2ddd-43c4-89dd-f36b302db1c9" />

Para el análisis he usado librerías como:
- **pandas:** trabajar con DataFrames
- **seaborn:** ajustar la apariencia general de los gráficos
- **re:** extraer números de una cadena
- **numpy:** hacer media de salarios
- **requests:** llamar API de GeoNames
- **google.colab:** usar variable de entorno para la api de GeoNames en google colab sin tener que exponer mi nombre de usuario
- **folium:** mostrar mapa de calor
- **matplotlib.pyplot:** mostrar gráficos

Además, he tenido que usar GeoNames para sacar las coordenadas de todas las ciudades que aparecen en mi tabla, y así poder pintarlos en el mapa de calor.

<img width="577" alt="Captura de pantalla 2025-04-01 a las 9 31 12" src="https://github.com/user-attachments/assets/b2db660f-1d80-4630-9566-d222507de6f4" />

Puedes ver los pasos y código del [EDA completo aquí📍.](https://github.com/alharuty/Proyecto-EDA-MiniDathaton/blob/main/Proyecto_IV_Datathon.ipynb)
Puedes ver el [EDA completo y la conclusión aquí📍.](https://github.com/alharuty/Proyecto-EDA-MiniDathaton/blob/main/EDA_Alla.pdf)

**Dame estrella⭐ en mi proyecto y apóyame**🤗
