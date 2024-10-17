import yfinance as yf
import numpy as np
import talib
import time

# Obtener los datos de precios de Yahoo Finance
def get_historical_data(symbol, period):
    """
    Obtiene los datos históricos de una acción o criptomoneda.
    """
    data = yf.download(symbol, period=period, interval='1h')
    close_prices = data['Close'].values
    return np.array(close_prices)

# Calcular el RSI
def calculate_rsi(prices, period=14):
    """
    Calcula el índice de fuerza relativa (RSI).
    """
    return talib.RSI(prices, timeperiod=period)

# Estrategia de compra/venta basada en RSI
def check_for_signal(rsi):
    """
    Señal de compra/venta basada en el valor del RSI.
    """
    if rsi[-1] < 30:
        return 'buy'
    elif rsi[-1] > 70:
        return 'sell'
    return None

# Simulación de compra/venta (sin órdenes reales)
def place_order(symbol, quantity, side):
    """
    Simula una orden de compra o venta.
    """
    print(f"Simulación de orden: {side} {quantity} {symbol}")
    return {'side': side, 'quantity': quantity, 'symbol': symbol}

# Parámetros del bot
symbol = 'BTC-USD'  # Par de trading (puedes cambiarlo por una acción como 'AAPL')
quantity = 0.001    # Cantidad ficticia a comprar/vender

# Bucle principal del bot
while True:
    # Obtener datos de precios históricos
    prices = get_historical_data(symbol, '1mo')  # Último mes de datos

    # Calcular RSI
    rsi = calculate_rsi(prices)
    
    # Comprobar si hay una señal de compra o venta
    signal = check_for_signal(rsi)
    
    if signal == 'buy':
        # Simulación de orden de compra
        place_order(symbol, quantity, 'BUY')
    elif signal == 'sell':
        # Simulación de orden de venta
        place_order(symbol, quantity, 'SELL')
    
    # Esperar un tiempo antes de la siguiente operación (por ejemplo, 1 hora)
    time.sleep(3600)

