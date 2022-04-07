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

        # ===== Create virtual ENV on python based platform=====
          181  echo ===== 2022.03.29 =====  
          # (1) Create virtual ENV jb_py307 (ALERT: do it once only)  
          185  cd ~
          188  python -m venv jb_py307 # ALERT: do it once only

          # (2) activate virtual ENV
          193  source ~/jb_py307/bin/activate

          # show prompt with (jb_py307) means using this venv  
          (jb_py307) pi@raspberrypi:~ $

          # (3) for example: try to install pandas into venv of jb_py307
          source ~/jb_py307/bin/activate
          200 (jb_py307) pi@raspberrypi:~ $  pip install pandas
          201 (jb_py307) pi@raspberrypi:~ $  pip show pandas

          # (4) deactivate virtual ENV of jb_307
          204  deactivate
          # show prompt without (jb_py307) means no venv now
          pi@raspberrypi:~ $ 
  
