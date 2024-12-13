mapa = gpd.read_file("mapa_comarcas_corregido.shp")  # Cambia por tu archivo Shapefile

 # Cargar el archivo CSV de salud mental
salud_comarcas = pd.read_csv("salud_mental_porcentajes.csv")

 # Asegurarse de que las columnas coincidan
print(mapa.columns)  # Revisa las columnas del Shapefile

print(salud_comarcas.columns)  # Revisa las columnas del CSV
# Renombrar columnas por si acaso
mapa = mapa.rename(columns={"nombre_comarca": "Comarca"})  # Cambia según el nombre real en el Shapefile
salud_comarcas = salud_comarcas.rename(columns={"Comarca": "Comarca"})  # Asegúrate de que coincide

# Unir los datos del CSV al GeoDataFrame del mapa
mapa_salud = mapa.merge(salud_mental_porcentajes, on="Comarca")

# Graficar el mapa
fig, ax = plt.subplots(1, 1, figsize=(10, 10))
mapa_salud.plot(column= "Porcentaje Salud Mental (%)", cmap="Blues", legend=True, ax=ax)

for idx, row in mapa_salud.iterrows():
centroid = row["geometry"].centroid
ax.text(
centroid.x, centroid.y,
f"{row['Porcentaje Salud Mental (%)']:.1f}%",
fontsize=6, color="grey", ha="center", va="center", weight="bold"
    )

# Personalización
ax.set_title("% de individuos con problemas de salud mental diagnosticada", fontsize=15)
ax.axis("off")

# Guardar el mapa como imagen (opcional)
plt.savefig("mapa_saludcita.png", dpi=300, bbox_inches="tight")

# Mostrar el mapa
plt.show()
