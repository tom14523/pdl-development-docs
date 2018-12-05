```Java
/**
 * BASE64编码转换的工具类
 */
public final class Base64Utils {

    /**
     * 文件读取缓冲区大小
     */
    private static final int CACHE_SIZE = 1024;

    /**
     * BASE64字符串解码为二进制数据
     *
     * @param base64 BASE64字符串
     * @return byte[] 解码后字节数组
     */
    public static byte[] decode(String base64) {
        return new Base64().decode(base64);
    }

    /**
     * 二进制数据编码为BASE64字符串
     *
     * @param bytes 二进制数据
     * @return String BASE64字符串
     */
    public static String encode(byte[] bytes) {
        return new Base64().encodeToString(bytes);
    }

    /**
     * 将文件编码为BASE64字符串
     * 大文件慎用，可能会导致内存溢出
     *
     * @param filePath 文件绝对路径
     * @return String BASE64字符串
     */
    public static String encodeFile(String filePath) {
        byte[] bytes = fileToByte(filePath);
        return encode(bytes);
    }

    /**
     * BASE64字符串转回文件
     *
     * @param filePath 文件绝对路径
     * @param base64   BASE64字符串
     */
    public static void decodeToFile(String filePath, String base64) {
        byte[] bytes = decode(base64);
        byteArrayToFile(bytes, filePath);
    }

    /**
     * 文件转换为二进制数组
     *
     * @param filePath 文件路径
     * @return byte[] 字节数组
     */
    public static byte[] fileToByte(String filePath) {
        byte[] data = new byte[0];
        File file = new File(filePath);
        if (!file.exists()) {
            return data;
        }

        try (FileInputStream in = new FileInputStream(file);
             ByteArrayOutputStream out = new ByteArrayOutputStream(2048)) {
            byte[] cache = new byte[CACHE_SIZE];
            int nRead = 0;
            while ((nRead = in.read(cache)) != -1) {
                out.write(cache, 0, nRead);
                out.flush();
            }

            return out.toByteArray();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    }

    /**
     * 二进制数据写文件
     *
     * @param bytes    二进制数据
     * @param filePath 文件路径
     */
    public static void byteArrayToFile(byte[] bytes, String filePath) {
        InputStream in = new ByteArrayInputStream(bytes);
        File destFile = new File(filePath);
        if (!destFile.getParentFile().exists()) {
            destFile.getParentFile().mkdirs();
        }

        OutputStream out = null;
        try {
            destFile.createNewFile();
            out = new FileOutputStream(destFile);
            byte[] cache = new byte[CACHE_SIZE];
            int nRead = 0;
            while ((nRead = in.read(cache)) != -1) {
                out.write(cache, 0, nRead);
                out.flush();
            }
        } catch (Exception e) {
            throw new RuntimeException(e);
        } finally {
            if (out != null) {
                try {
                    out.close();
                } catch (IOException e) {
                }
            }

            if (in != null) {
                try {
                    in.close();
                } catch (IOException e) {
                }
            }
        }
    }
}
```
