# mmWave-notes

win = pg.GraphicsLayoutWidget(show=True) # pg.GraphicsWindow() deprecated



# MQTT installation:
    pip install paho-mqtt
    pip3 install paho-mqtt
    
    

# mosquitto configure file location(synology NAS) :
    $cd /volume1/@appstore/mosquitto/var/
    $ls
    mosquitto.conf
    
    /var/packages/mosquitto/
    
    
# Create python virtual ENV 
      
      # (step 01) Create virtual ENV named 'jb_py307' (ALERT: do this step once only)  
      
      cd ~
      python -m venv jb_py307       # ALERT: do it once only

      # (step 02) Activate virtual ENV
      
      source ~/jb_py307/bin/activate

      # after activated show prompt with '(jb_py307)' means using this venv  
      
      (jb_py307) pi@raspberrypi:~ $

      # (step 03) Try to install 'pandas' (for example) into venv of jb_py307
      
      source ~/jb_py307/bin/activate
      (jb_py307) pi@raspberrypi:~ $  pip install pandas         # will be installed in jb_py307 venv 
      (jb_py307) pi@raspberrypi:~ $  pip show pandas            # show file location

      # (4) Deactivate virtual ENV of jb_307
      
      (jb_py307) pi@raspberrypi:~ $ deactivate
      
      # after deactivated then show prompt without '(jb_py307)' means no venv now
      
      pi@raspberrypi:~ $ 
      

# Create Geany project for python virtual enviroment 
    
    # (step 01) Verify Geany setup
                on Geany selected /Edit/Preferences/General/Miscellaneous/Projects
                selected both of "Use project ..." and "Store project ..."  

    # (step 02) Create project name, for example: 'jb_g10.geany' 
                selected /Project/New for '/home/pi/jb_py307/jb_g10.geany' 
                for example: virtual env name is "jb_py307"
                             project name is "jb_g10"

    # (step 03) Set dedicated python.exe path, for example: based on venv 'jb_py307' 
                selected /Build/Set Build Commands/ 
                for example: on Compile field, filled /home/pi/jb_py307/bin/python3-m py_compile "%f"  
                for example: on Excute  field, filled /home/pi/jb_py307/bin/python3 "%f" 

# Run RPi Z2W program on startup

    # (step 01) Added startup file: '/home/pi/.config/autostart/jb_g10_startup.desktop' 
        file content:
        [Desktop Entry]
        Type=Application
        Name=jb_g10_startup_name
        Exec=xterm -hold -sb -e 
             'sudo chmod 777 /dev/ttyS*; 
             ls -l /dev/ttyS*; 
             cd /home/pi/Desktop/G01Parking/G10Parking-main; 
             /home/pi/jb_py307/bin/python3 /home/pi/Desktop/G01Parking/G10Parking-main/jb_g10_startup.py'
        
        # ALERT: above 'Exec' command line just for easy reading purpose should not be inserted 'new line'
        # Here 'jb_py307' is venv folder, means based on python 3.07
        
        # Refer: https://learn.sparkfun.com/tutorials/how-to-run-a-raspberry-pi-program-on-startup/all#method-2-autostart     
    
    # (step 02) Working app: '/home/pi/Desktop/G01Parking/G10Parking-main/jb_g10_startup.py'
   
   
   
 ## calculate doppler to speed or Hz

         Calculate the radial velocity of an automobile based on the Doppler shift of a continuous-wave radar. 
         The radar carrier frequency is 61.25 GHz.  
            
            doppler convert to Hz
            # fd = -2V/λ  where λ = c/f
            # fd = -2 * c/f * V = -2 * Doppler/(3 * 1e8 / 61.25 * 1e9 ) 
            # ex: fd(Hz) = -2 * Doppler/ 0.00489796  
            #            = -408.3632 * Doppler
            #
            
            Doppler unit: m/sec
            convert to km/hr 
            speed(km/hr) = doppler * (1000/3600)
            
 ## Antenna Array of Two Isotropic Point Sources in Same Phase
    
    https://www.youtube.com/watch?v=cuch5ZmyyvI&t=73s


## GLMeshItem plot

        w3 = gl.GLViewWidget()
        w3.setWindowTitle('(w3) v1020 xy pointCloud(sp1) / JB_v7 Object(sp3)')
        w3.show()
        
        
        def radarBoxVertexes(height = None):
            verX = 0.0625
            verY = 0.05
            verZ = 0.125
            zOffSet = height
            verts = np.empty((2,3,3))
            verts[0,0,:] = [-verX, 0, verZ + zOffSet]
            verts[0,1,:] = [-verX, 0,-verZ + zOffSet]
            verts[0,2,:] = [verX,  0,-verZ + zOffSet]
            verts[1,0,:] = [-verX, 0, verZ + zOffSet]
            verts[1,1,:] = [verX,  0, verZ + zOffSet]
            verts[1,2,:] = [verX,  0, -verZ + zOffSet]
            return verts

        evmBox = gl.GLMeshItem(vertexes=radarBoxVertexes(height = install_height) ,smooth=False,drawEdges=True,edgeColor=pg.glColor('r'),drawFaces=False)

        w3.addItem(evmBox)

        update:
        evmBox.setMeshData(vertexes=radarBoxVertexes(height=JB_RADAR_INSTALL_HEIGHT),smooth=False,drawEdges=True,edgeColor=pg.glColor('r'),drawFaces=False)

## mmWave Radar Sensors: Object Versus Range application notes:

    https://www.ti.com/lit/an/swra593a/swra593a.pdf?ts=1683599374296&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252Fzh-tw%252FAWR6843
