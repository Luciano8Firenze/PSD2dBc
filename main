import numpy as np
from scipy.integrate import quad
from scipy import constants

# 将数据转换为numpy数组
amplitude = np.array(data['x'])
frequency = np.array(data['y'])

# 将幅度单位转换为dBc/Hz
amplitude = 10**(amplitude/10)

# 定义测量时间T和延迟时间τ
T = 1  # 需要根据实际情况进行设定
tau = 1  # 需要根据实际情况进行设定

# 计算S_delta_phi(f)
S_delta_phi = amplitude * T

# 计算S_phi(f)
S_phi = S_delta_phi / (2 * np.sin(np.pi * frequency * tau))**2

# 计算S_v(f)
S_v = frequency**2 * S_phi

# 定义积分函数
def integrand(f):
    beta_line = 8 * np.log(2) * f / constants.pi**2
    return np.heaviside(S_v - beta_line, 0.5) * S_v

# 计算区域A
A, error = quad(integrand, 1/T, np.inf)

# 计算FWHM
FWHM = np.sqrt(8 * np.log(2) * A)
print('The FWHM of the laser is: ', FWHM, 'Hz')
