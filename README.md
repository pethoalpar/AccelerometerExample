# Androi accelerometer example

```java
public class MainActivity extends AppCompatActivity implements SensorEventListener {

    private TextView textView;
    //Sensor manager

    private SensorManager sensorManager;
    private Sensor accelerometerSensor;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        textView = (TextView) this.findViewById(R.id.textView);

        sensorManager = (SensorManager) getSystemService(Context.SENSOR_SERVICE);
        accelerometerSensor = sensorManager.getDefaultSensor(Sensor.TYPE_ACCELEROMETER);
        sensorManager.registerListener(this, accelerometerSensor, SensorManager.SENSOR_DELAY_UI);
    }

    @Override
    public void onSensorChanged(SensorEvent event) {
        if(event.sensor.getType() != Sensor.TYPE_ACCELEROMETER){
            return;
        }
        float x = event.values[0];
        float y = event.values[1];
        float z = event.values[2];
        double angle = (Math.atan2(y, Math.sqrt(x*x+z*z))/ (Math.PI / 180));
        StringBuilder sb = new StringBuilder().append("x:").append(x).append("\n");
        sb.append("y:").append(y).append("\n");
        sb.append("z:").append(z).append("\n");
        sb.append("degree:").append(angle);
        textView.setText(sb.toString());
    }

    @Override
    public void onAccuracyChanged(Sensor sensor, int accuracy) {

    }
}
```
