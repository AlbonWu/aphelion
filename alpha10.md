
```

import java.awt.*;
import java.awt.event.*;
import java.io.*;
import java.util.*;
import java.util.logging.Level;
import java.util.logging.Logger;

import javax.swing.*;
import javax.swing.border.*;
import javax.swing.filechooser.FileSystemView;
import javax.swing.filechooser.FileView;

public class wordProcessor extends JFrame {

	private JPanel contentPane;
	private JFileChooser fc = new JFileChooser();

	@SuppressWarnings("resource")
	public wordProcessor() throws IOException {
		super("Aphelion Notepad");
		setIconImage(Toolkit.getDefaultToolkit().getImage("C:\\Users\\Albon Wu\\Downloads\\imageedit_1_8173875007.png"));
		setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		setBounds(100, 100, 450, 300);

		contentPane = new JPanel();
		contentPane.setBackground(Color.WHITE);
		contentPane.setBorder(new EmptyBorder(5, 5, 5, 5));
		contentPane.setLayout(new BorderLayout(0, 0));
		setContentPane(contentPane);

		JTextArea textArea = new JTextArea();
		textArea.setLineWrap(true);
		contentPane.add(textArea, BorderLayout.CENTER);
		textArea.setFont(new Font("Arial", 20, 20));

		String getInput = textArea.getText();

		JMenuBar menuBar = new JMenuBar();
		setJMenuBar(menuBar);

		JButton save = new JButton("Save\r\n");
		save.setIcon(new ImageIcon(
				wordProcessor.class.getResource("/com/sun/java/swing/plaf/windows/icons/FloppyDrive.gif")));
		menuBar.add(save);
		save.setBackground(Color.WHITE);
		JButton open = new JButton("Open");
		open.setIcon(
				new ImageIcon(wordProcessor.class.getResource("/com/sun/java/swing/plaf/windows/icons/UpFolder.gif")));
		menuBar.add(open);
		open.setBackground(Color.WHITE);
		menuBar.setBackground(Color.WHITE);

		open.addActionListener(new ActionListener() {
			File selectedFile;

			@Override
			public void actionPerformed(ActionEvent arg0) {

				final JFileChooser fc = new JFileChooser();
				int returnVal = fc.showOpenDialog(open);
				selectedFile = fc.getSelectedFile();

				try {
					Scanner file = new Scanner(new FileInputStream(selectedFile));
					String temp = "";
					while (file.hasNext()) {
						temp += file.nextLine();
					}
					textArea.setText(temp);
					file.close();
				} catch (FileNotFoundException e) {

					e.printStackTrace();
				}
			}
		});
		save.addActionListener(new ActionListener() {

			@Override
			public void actionPerformed(ActionEvent arg0) {
				try {
					PrintWriter pw = new PrintWriter(new File("input.in"));
					pw.println(textArea.getText());
					pw.close();
				} catch (FileNotFoundException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}

			}
		});

	}

	public static void main(String[] args) {

		EventQueue.invokeLater(new Runnable() {
			public void run() {
				try {
					wordProcessor frame = new wordProcessor();
					frame.setVisible(true);
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		});

	}

}

```
