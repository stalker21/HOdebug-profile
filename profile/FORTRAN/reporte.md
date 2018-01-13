
Se compilo el archivo loop-interch.f90 con cuatro  opciones de optimización (O0,O1, O2, O3) y luego se ejecutó cada archivo con time. El tiempo de ejecución mejoró significativamente con la opción de optimización O3, como se ve a continuación:
 
loop-interch-O0 (opt O0)

real	0m10.931s
user	0m10.768s
sys	0m0.140s

loop-interch-O1 (opt O1)

real	0m10.782s
user	0m10.568s
sys	0m0.192s

loop-interch-02 (opt 02)

real	0m11.109s
user	0m10.864s
sys	0m0.188s


loop-interch-03 (opt O3)

real	0m3.020s
user	0m2.824s
sys	0m0.156s

Por último se intentó compilar y ececutar con time y gprof los archivos en c pero devolvían el error segmentation fault. Se intentó utilizar gprof en fortran pero los resportes dieron vacíos. Para utilizar perf se necesitaron permisos. 

