package weather.forecast.main;

import java.awt.Color;
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.util.ArrayList;

import javax.json.JsonArray;
import javax.json.JsonObject;
import javax.swing.JFrame;
import javax.swing.JList;
import javax.swing.SwingUtilities;

import weather.forecast.DetailedCity.CurrentWeatherDialog;
import weather.forecast.DetailedCity.ForecastWeatherDialog;
import weather.forecast.MainMenu.BackgroundPanel;
import weather.forecast.MainMenu.CityResultDialog;
import weather.forecast.MainMenu.SearchPanel;

/**
 *
 */
public class MainMenuFrame extends JFrame {
    private JsonArray dataCurrWeather;
    public JsonArray getDataCurrWeather(){
        return dataCurrWeather;
    }
    public void setDataCurrWeather(JsonArray dataCurrWeather){
        this.dataCurrWeather = dataCurrWeather;
    }
    
    private JsonArray dataForecastWeather;
    public JsonArray getDataForecastWeather(){
        return dataForecastWeather;
    }
    public void setDataForecastWeather(JsonArray dataForecastWeather){
        this.dataForecastWeather = dataForecastWeather;
    }
    
    private SearchPanel searchPanel;
    public SearchPanel getSearchPanel(){
        return searchPanel;
    }
    
    private CityResultDialog cityResultDialog;
    public CityResultDialog getCityResultDialog(){
        return cityResultDialog;
    }
    
    private CurrentWeatherDialog currentWeatherDialog;
    public CurrentWeatherDialog getCurrentWeatherDialog(){
        return currentWeatherDialog;
    }

    private JsonObject currSelectedCity;
    public JsonObject getCurrSelectedCity(){
        return currSelectedCity;
    }
    public void setCurrSelectedCity(JsonObject obj){
        currSelectedCity = obj;
    }
    
    private ForecastWeatherDialog forecastWeatherDialog;
    public ForecastWeatherDialog getForecastWeatherDialog(){
        return forecastWeatherDialog;
    }
    
    private JsonObject forecastSelectedCity;
    public JsonObject getForecastSelectedCity(){
        return forecastSelectedCity;
    }
    
    private SelectCityListener selectCityListener;
    public SelectCityListener getSelectCityListener(){
        return selectCityListener;
    }
    
    private ForecastWeatherClickListener forecastWeatherClickListener;
    public ForecastWeatherClickListener getForecastWeatherClickListener(){
        return forecastWeatherClickListener;
    }
    
    public void setForecastSelectedCity(JsonObject obj){
        forecastSelectedCity = obj;
    }
    
    public MainMenuFrame(String title){
        super(title);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
    
        //set Backgorund
        BackgroundPanel background= new BackgroundPanel();
        background.setLayout(new GridBagLayout());
        this.add(background);
        
        SearchClickListener searchClickListener = new SearchClickListener(this);
        searchPanel = new SearchPanel(searchClickListener);
        searchPanel.setBackground(new Color(255, 255,255, 0));
        GridBagConstraints c= new GridBagConstraints();
        c.gridx=0;
        c.gridy=0;
        background.add(searchPanel,c);
        this.pack();
        this.setSize(800, 600);
        this.setLocationRelativeTo(null);
//        container.add(cityResultPanel, BorderLayout.CENTER);
        
        setVisible(true);
    }
    
    public void initializeCityResultDialog(){
        cityResultDialog = new CityResultDialog(this, true);
    }
    
    public void initializeCurrentWeatherDialog(){
        currentWeatherDialog = new CurrentWeatherDialog(this, true);
    }
    
    public void initializeSelectCityListener(ArrayList<String> list_selection, JList<String> list_city){
        selectCityListener = new SelectCityListener(this, list_selection, list_city);
    }
    
    public void initializeForecastWeatherClickListener(){
        forecastWeatherClickListener = new ForecastWeatherClickListener(this);
    }
    
    public void initializeForecastWeatherDialog(){
        forecastWeatherDialog = new ForecastWeatherDialog(this, true, forecastSelectedCity);
    }
    
    
    public static void main(String[] args){
        SwingUtilities.invokeLater(new Runnable(){
            public void run(){
                MainMenuFrame frame = new MainMenuFrame("Weather Forecast");
            }
        });
    }
}