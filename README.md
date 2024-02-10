
java
import com.google.zxing.*;
import com.google.zxing.client.j2se.BufferedImageLuminanceSource;
import com.google.zxing.common.HybridBinarizer;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.util.HashMap;
import java.util.Map;

public class BarcodeReader {

    public static void main(String[] args) {
        try {
            // اختيار صورة من الاستوديو
            File imageFile = new File("path/to/your/image.jpg");
            BufferedImage image = ImageIO.read(imageFile);

            // قراءة الباركود من الصورة
            String barcodeValue = readBarcode(image);

            // عرض قيمة الباركود
            System.out.println("تم قراءة الباركود: " + barcodeValue);

            // يمكنك إضافة هنا المزيد من الخطوات مثل مشاركة القراءة إلخ
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private static String readBarcode(BufferedImage image) throws NotFoundException {
        BinaryBitmap binaryBitmap = new BinaryBitmap(
                new HybridBinarizer(new BufferedImageLuminanceSource(image))
        );

        Map<DecodeHintType, Object> hints = new HashMap<>();
        hints.put(DecodeHintType.TRY_HARDER, Boolean.TRUE);

        Result result = new MultiFormatReader().decode(binaryBitmap, hints);
        return result.getText();
    }
}


